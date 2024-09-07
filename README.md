pip install sphinx
pip install sphinx-book-theme

make html

python3 -m http.server --directory _build/html
