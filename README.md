## Resume Information Extraction using NLP (Named Entity Recognition)

This project implements an NLP pipeline to automatically extract structured data such as Name, Skills, Degree, Institutions, and Work Experience from resumes using SpaCy's Named Entity Recognition (NER). It supports both .txt and .pdf formats and demonstrates how NER and regex can be combined to build a smart resume parser.

## 🚀 Features
Preprocesses a JSON dataset of annotated resumes

Converts annotations into SpaCy training format

Trains a custom NER model using spacy.blank()

Handles overlapping/misaligned entity spans

Supports resume input in .txt and .pdf formats

## Uses regex for email, phone, and LinkedIn extraction

## 🧠 Extracted Entities
Name

Skills

Degree

College Name

Graduation Year

Email

Phone number

LinkedIn

## 📂 Project Structure
```
├── NER.ipynb                      # Main notebook: data loading, training, and testing
├── Entity Recognition in Resumes.json   # Annotated dataset
├── Sample Resume.pdf/.txt         # For testing purposes
├── negan.pdf                      # Report (summary of model and results)
```
## 🛠️ Dependencies

Make sure to install the following:

```
pip install spacy==3.x
pip install pdfplumber
pip install pymupdf
```
## Also required:

re, random, and other standard Python libraries

## 📌 How to Run
1.Upload the JSON dataset
2.Open and run each cell in NER.ipynb
3.Train the custom NER model
4.Test it on .txt or .pdf resumes

## 🧪 Example: Testing a TXT Resume

with open("your_resume.txt", "r", encoding="utf-8") as f:
    resume_text = f.read()

doc = nlp(resume_text)
for ent in doc.ents:
    print(f"{ent.label_:<25} ➤ {ent.text}")
## 🧪 Example: Testing a PDF Resume
```
import spacy
import pdfplumber
import re
from collections import defaultdict
import json

# Load your trained spaCy NER model
model_path = "/content/ner_resume_model"
nlp = spacy.load(model_path)
print("✅ Model loaded successfully.")

# Load and read text from PDF
pdf_path = "/content/negan.pdf"  # Replace with your file path
text = ""
with pdfplumber.open(pdf_path) as pdf:
    for page in pdf.pages:
        text += page.extract_text() + "\n"

# Use your NER model
doc = nlp(text)

# Extract entities from model
entities = defaultdict(list)
for ent in doc.ents:
    entities[ent.label_].append(ent.text.strip())

print("\n📄 Extracted Entities from PDF:")
for label, values in entities.items():
    for val in values:
        print(f"{val} ➤ {label}")

# Regex Post-processing
email_match = re.search(r'[\w\.-]+@[\w\.-]+', text)
phone_match = re.search(r'\+91[-\s]?[0-9]{10}', text)
linkedin_match = re.search(r'linkedin\.com\/[^\s]+', text)

print("\n🔧 Regex Post-processing:")
if email_match:
    print(f"Email ➤ {email_match.group()}")
if phone_match:
    print(f"Phone ➤ {phone_match.group()}")
if linkedin_match:
    print(f"LinkedIn ➤ {linkedin_match.group()}")print(f"LinkedIn ➤ {linkedin_match.group()}")
```

## Sample Output

## output 1
<img width="370" height="161" alt="image" src="https://github.com/user-attachments/assets/eaea3f73-4315-4758-b285-0043d3524ca1" />

## output 2
<img width="518" height="200" alt="image" src="https://github.com/user-attachments/assets/e6cb5083-ca6a-418c-811b-fd7010f18ac5" />

## 📸 Visual Output
✅ Extracted Entities from .txt Resumes

✅ Extracted Entities from .pdf Resumes

✅ Display in console (can be extended to GUI using Streamlit)

## 📌 Notes
Misaligned spans are automatically skipped

Clean, consistent annotations boost accuracy

Custom NER model performance depends on quality & coverage of training data

## 💡 Future Enhancements
Improve training data with better alignment

Fine-tune on pre-trained SpaCy pipelines

Integrate with Streamlit for GUI-based resume upload and extraction

## Conclusion
This project demonstrates how NLP + NER can be used to convert unstructured resumes into structured information. With additional regex logic and PDF processing support, it’s a solid foundation for resume analysis tools in recruitment or HR automation.
