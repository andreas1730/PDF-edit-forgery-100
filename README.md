# PDF-edit-forgery-100

**100 paired genuine and edited PDF documents, with edit-location annotations.**

**Creator:** Andreas

PDF-edit-forgery-100 brings together 100 genuine source PDFs and 100 synthetically edited counterparts. Each pair shares a stable identifier, from `P001` to `P100`, making it straightforward to compare the documents and locate the described changes.

The collection includes financial, regulatory, audit, government, contractual, and court-related documents. A single English edit guide explains what was changed, where it was changed, and the original and edited values.

## At a glance

| Item | Count / format |
| --- | --- |
| Document pairs | 100 |
| Genuine documents | 100 PDFs |
| Edited documents | 100 PDFs |
| Edit guide | `EDIT_LOCATIONS.txt` |
| Pair identifiers | `P001`–`P100` |
| Annotation language | English |
| Page numbering | One-based |

## Download

The distribution archive is named **`PDF-edit-forgery-100.zip`**. Once the release is public, download it from this repository's [Releases](../../releases) page and extract it.

The archive contains only the paired documents and the edit guide. This README provides the repository documentation separately.

```text
genuine/
    P001_...pdf
    ...
    P100_...pdf
forged/
    P001_..._FORGED.pdf
    ...
    P100_..._FORGED.pdf
EDIT_LOCATIONS.txt
```

The repository also contains a copy of `EDIT_LOCATIONS.txt` for convenient browsing.

## How the pairs work

Use the **pair ID at the beginning of each filename** to match documents. For example, a genuine PDF beginning with `P001_` corresponds to the edited PDF beginning with `P001_` in `forged/`.

- **`genuine/`** contains the source documents used for each pair.
- **`forged/`** contains the corresponding synthetically edited documents.
- **`EDIT_LOCATIONS.txt`** describes the changes for all 100 pairs.

The labels describe each file's role in this collection. The edited versions were prepared as document-editing examples; they are not presented as evidence of wrongdoing by the original issuers or named individuals.

## Edit-location guide

Each entry in `EDIT_LOCATIONS.txt` includes:

| Field | Meaning |
| --- | --- |
| Pair ID and title | Identifies the document pair |
| Original | Relative path to the genuine PDF |
| Altered | Relative path to the edited PDF |
| Edited page | Page containing the described edit, starting at 1 |
| Field | The document field or content that was changed |
| Before | Original value |
| After | Edited value |
| Change | Brief English description of the alteration |

The guide supplies page and field references rather than pixel coordinates or segmentation masks. It helps readers navigate a pair without adding separate annotation files for every document.

## Document categories

Counts refer to **pairs**, with one genuine PDF and one edited PDF in each pair.

| Category | Pairs |
| --- | ---: |
| Audit reports | 24 |
| Enforcement or court documents | 17 |
| Financial statements or annual reports | 15 |
| Government notices or letters | 12 |
| Bank regulatory reports | 9 |
| Bank statements | 6 |
| Tax or government forms | 6 |
| Contracts or agreements | 2 |
| Loan or credit documents | 2 |
| Invoices or payment documents | 1 |
| Other documents | 6 |
| **Total** | **100** |

## Getting started

1. Extract `PDF-edit-forgery-100.zip`.
2. Open `EDIT_LOCATIONS.txt` and choose a pair ID.
3. Open the matching PDFs from `genuine/` and `forged/` side by side.
4. Navigate to the listed page and compare the described field and values.

No specialized software is required for manual comparison beyond a PDF viewer.

To check the pairing with Python, run the following from the extracted dataset directory:

```python
from pathlib import Path

root = Path(".")
genuine = {p.name.split("_", 1)[0]: p for p in (root / "genuine").glob("*.pdf")}
forged = {p.name.split("_", 1)[0]: p for p in (root / "forged").glob("*.pdf")}
expected = {f"P{i:03d}" for i in range(1, 101)}

assert len(list((root / "genuine").glob("*.pdf"))) == 100
assert len(list((root / "forged").glob("*.pdf"))) == 100
assert genuine.keys() == forged.keys() == expected
print("100 matching PDF pairs found.")
```

## Using the dataset

The paired structure supports document comparison, PDF editing analysis, annotation inspection, and educational examples. The original and edited PDFs can be examined visually or with PDF-processing tools.

- Keep each original and its edited counterpart together when organizing experiments.
- If creating training and evaluation partitions, group related source documents to reduce overlap.
- Preserve the distributed PDF bytes when studying document structure or editing traces. Re-exporting a PDF can change those properties.
- Page and field annotations describe the listed alterations; they do not provide an exhaustive inventory of every internal PDF-object difference.

## Sources and licensing

Source documents were obtained from publicly accessible government, regulatory, court, and organizational sources.

**CC BY 4.0 applies only to original annotations and contributions owned by Andreas.** See [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/).

Third-party source documents retain their applicable rights. This notice grants no additional rights in third-party or public-domain material. Public accessibility does not itself establish redistribution permission. Copyright licensing also does not grant privacy or publicity rights.

## Version and maintenance

This is a fixed collection of 100 pairs. No scheduled updates are planned. Corrections or future versions can be tracked through this repository's releases and issues.

For questions or to report an annotation problem, open an [issue](../../issues) and include the pair ID, the field in question, and a brief description.

## Acknowledgment

When referring to the collection, use **PDF-edit-forgery-100** and credit **Andreas**. A DOI or formal citation can be added when available.
