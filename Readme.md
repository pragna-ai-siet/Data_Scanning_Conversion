# Data_Scanning_Conversion

This directory contains all scripts and files for converting 1700+ Kannada PDFs into clean, structured JSON chunks suitable for fine-tuning and search.

The process includes PDF rendering, OCR, cleaning, and formatting.

---

## Folder Structure

- `raw_pdfs/` — Original PDFs (books, scanned documents)
- `page_images/` — Images extracted from PDFs (one image per page)
- `ocr_output_txt/` — Raw OCR output from each page (usually noisy)
- `cleaned_text/` — Text after cleaning, normalization, and deduplication
- `json_chunks/` — Final structured text chunks (for model training or retrieval)
- `scripts/` — All automation scripts (PDF to image, OCR, cleaning, chunking)

---

## Data Conversion Pipeline (Step-by-Step)

1. **Drop Your PDFs**
   - Place all scanned or text-based PDFs in `raw_pdfs/`

2. **Convert PDFs to Images**
   - Use scripts in `scripts/` to turn each page into an image
   - Tools used: `pdf2image`, `pdftoppm`, or `pypdfium2`
   - Output saved in `page_images/`

3. **Run OCR on Images**
   - Choose between:
     - `Tesseract OCR` (with Kannada language pack)
     - `Surya OCR` (GPU-accelerated and layout-aware)
   - Run OCR in batch on all images
   - Output saved in `ocr_output_txt/`

4. **Clean the OCR Output**
   - Remove special characters, normalize Unicode, fix spacing
   - Use `Indic NLP Library` or custom scripts
   - Save cleaned paragraphs into `cleaned_text/`

5. **Split Text into Chunks**
   - Divide large files into smaller passages (~200–400 tokens)
   - Add metadata (book title, page number, etc.)
   - Save chunks in `json_chunks/` in this format:
     ```json
     {
       "text": "cleaned Kannada text chunk",
       "meta": {
         "book_id": "Book-001",
         "page": 42
       }
     }
     ```

6. **Review and Prepare for Training**
   - Final files in `json_chunks/` are used in:
     - Fine-tuning datasets
     - Search index (TF-IDF or Vector DB)

---

## Tools & Dependencies

- `pdf2image`, `poppler-utils`, or `pypdfium2` — PDF to image
- `Tesseract OCR` or `Surya OCR` — Kannada text extraction
- `Indic NLP Library` — Unicode normalization and script-specific cleaning
- `Python` (3.8+) with libraries: `os`, `glob`, `Pillow`, `tqdm`, `json`, `re`

---
