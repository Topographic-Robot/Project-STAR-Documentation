Register Transfer Level (RTL)
=============================

Register Transfer Level (RTL) design focuses on the flow of data between registers and the logic operations performed on that data. It is critical in hardware description languages (HDL) such as Verilog and VHDL, where the code describes the behavior of digital circuits at the register level. In this project, we follow strict RTL guidelines to ensure clarity, reliability, and maintainability of the hardware design.

Guidelines
----------

- **Always Use Non-blocking Assignments for Sequential Logic**: For sequential logic (inside `always` blocks sensitive to a clock edge), use non-blocking assignments (`<=`) to ensure the correct behavior of registers and avoid race conditions.

  Correct Example:

  .. code-block:: verilog

    always @(posedge clk) begin
      if (reset)
        counter <= 0;
      else
        counter <= counter + 1;
    end

  Incorrect Example:

  .. code-block:: verilog

    always @(posedge clk) begin
      if (reset)
        counter = 0;  /* Blocking assignment, incorrect for sequential logic */
      else
        counter = counter + 1;
    end

- **Use Blocking Assignments for Combinational Logic**: For combinational logic, use blocking assignments (`=`) within `always` blocks. This ensures that the logic is evaluated sequentially, and the output reflects the latest input conditions.

  Correct Example:

  .. code-block:: verilog

    always @(*) begin
      result = a + b;  /* Blocking assignment for combinational logic */
    end

  Incorrect Example:

  .. code-block:: verilog

    always @(*) begin
      result <= a + b;  /* Non-blocking assignment in combinational logic */
    end

- **Keep the Clock Domain Clean**: Ensure that logic within one clock domain does not inadvertently interact with another clock domain. Use appropriate synchronizers and clock domain crossing techniques to prevent metastability.

  Example of Clock Domain Crossing:

  .. code-block:: verilog

    always @(posedge clk1 or posedge reset) begin
      if (reset)
        sync_reg <= 0;
      else
        sync_reg <= async_signal;
    end

    always @(posedge clk2) begin
      sync_output <= sync_reg;
    end

- **Use Descriptive Signal Names**: Avoid generic names like `temp`, `signal1`, etc. Choose meaningful signal names that clearly indicate the function and purpose of the signal.

  Correct Example:

  .. code-block:: verilog

    reg [7:0] data_in;   /* Clear and descriptive */
    reg [7:0] data_out;  /* Output of the data */

  Incorrect Example:

  .. code-block:: verilog

    reg [7:0] temp;   /* Ambiguous and unclear */
    reg [7:0] sig1;   /* Non-descriptive */

- **Follow a Consistent Reset Strategy**: Always ensure that reset behavior is consistent across the design. Use synchronous or asynchronous resets depending on the design requirements, and clearly document the reset behavior.

  Correct Example (Synchronous Reset):

  .. code-block:: verilog

    always @(posedge clk) begin
      if (reset)
        data_reg <= 0;
      else
        data_reg <= next_data;
    end

  Incorrect Example:

  .. code-block:: verilog

    always @(posedge clk or posedge reset) begin
      if (reset)
        data_reg <= 0;
      else
        data_reg = next_data;  /* Incorrect use of blocking assignment */
    end

- **Document RTL Code Clearly**: Each module should include a comment block explaining its functionality, inputs, and outputs. Key design choices, such as pipeline stages or timing constraints, should be documented as well.

RTL Design Examples
-------------------

Correct Example (Sequential Logic with Non-blocking Assignments):

.. code-block:: verilog

  module counter (
      input  wire clk,
      input  wire reset,
      output reg  [3:0] count
  );

  always @(posedge clk or posedge reset) begin
    if (reset)
      count <= 0;
    else
      count <= count + 1;
  end

  endmodule

Incorrect Example (Blocking Assignment in Sequential Logic):

.. code-block:: verilog

  module counter (
      input  wire clk,
      input  wire reset,
      output reg  [3:0] count
  );

  always @(posedge clk or posedge reset) begin
    if (reset)
      count = 0;  /* Incorrect use of blocking assignment */
    else
      count = count + 1;
  end

  endmodule

General Guidelines
------------------

- **Use non-blocking assignments (`<=`) for sequential logic** inside clocked processes.

- **Use blocking assignments (`=`) for combinational logic**.

- **Ensure proper clock domain crossings** using synchronizers.

- **Name signals descriptively** to improve code readability and maintainability.

- **Keep reset strategy consistent** across the design.

- **Document modules and key decisions** within the RTL code.

