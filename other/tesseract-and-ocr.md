# Tesseract & OCR

## Tesseract

[About optimal resolution/DPI](https://groups.google.com/g/tesseract-ocr/c/Wdh_JJwnw94/m/24JHDYQbBQAJ)

[Improving Quality docs](https://tesseract-ocr.github.io/tessdoc/ImproveQuality.html)

* Tesseract 4.x needs dark text on light background \(3.x did not have this limitation\).

```text
# Extract text to stdout from image.png using only abc characters
tesseract image.png stdout -c tessedit_char_whitelist=abc
```

