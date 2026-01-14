# chatGPTTranslate
This code is a minimal example on how to run a translation from an input .pdf or .docx file.
It requires having an account in chatGPT and setting up an API Key, there are multiple tutorials
online on how to do this. Note it's also not free, you need to have some credit in your account, but it's not expensive.
Once you've got your API Key, open powershell and type:

setx OPENAI_API_KEY "sk-XXXXXXXXXXXXXXXX"

where "sk-XXXXXXXXXXXXXXXX" is the API key you obtain. You might also need to install a few libraries, assuming
Python is installed, you can run the following (I used Python 3.11): 

pip install python-docx openai tiktoken PyMuPDF PyPDF2 pdfplumber ntlk
nltk.download("punkt")
nltk.download("punkt_tab")

The function "translate_chunk" contains the system prompt: 

                "content": (
                    "You are a professional literary translator. "
                    "Translate the following text from Spanish to English, "
                    "preserving tone, style, and paragraph structure. "
                    "Do not summarize or omit any content."
                )

It's set for translating from Spanish to English, but can of course be modified for any language you might need. 
The function chunk_paragraphs slices the input file in chunks that would not exceed the token limit for a single
chatGPT query. The model chosen by default is "gpt-4o-mini" which, in my experience, provides a decent translation
for a small price: translating a 450-500 page book cost me around 20-25 cents of a dollar. You can change the default values
here: 

chunk_paragraphs(paragraphs, max_tokens=1500, model="gpt-4o-mini")

Or when calling the function, you can specify it as arguments. In here you can choose the input an output file: 

    translate_book(
        input_file=$path_to_input_file,
        output_docx=$path_to_output_file,
        SLEEP_SECONDS
    )

Note the output file will be a .docx, but the input file can be a .docx (preferred) or a PDF (assuming the text in the PDF is extractabled, eg not an image)