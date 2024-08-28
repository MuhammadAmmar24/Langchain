# Text Splitters in LangChain

Text splitters in LangChain are used to divide large text into smaller chunks, making it easier to process by language models or to perform specific operations like indexing or vector embedding. Different splitters are optimized for various types of text, such as HTML, Markdown, code, or even plain text.

## Common Text Splitters in LangChain

1. **Recursively Split Text**
   - This splitter divides text recursively based on specified delimiters or characters, allowing for hierarchical splitting.

   ```python
   from langchain_core.text_splitter import RecursiveTextSplitter

   text = "This is a long document that needs splitting."
   splitter = RecursiveTextSplitter(delimiters=["\n\n", "\n", ". "])
   chunks = splitter.split_text(text)
   print(chunks)
   ```

2. **Recursive Character Text Splitter**
   - The `RecursiveCharacterTextSplitter` is an advanced splitter that recursively divides text based on characters. It starts by splitting the text using larger chunks (like paragraphs), and if the resulting chunks are still too large, it continues splitting into smaller pieces (like sentences, then words). This ensures the text is split into manageable pieces without breaking the semantic context unnecessarily.

   **Parameters:**
   - `chunk_size`: The maximum size of each chunk after splitting.
   - `chunk_overlap`: The number of characters that overlap between chunks. This is useful for ensuring context isn't lost between chunks.
   - `length_function`: A function that determines the length of a text. By default, it uses the character count.
   - `separators`: A list of characters used to split the text. The function starts with the first separator and moves to the next if the chunks are too large.

   **Example:**

   ```python
   from langchain_core.text_splitter import RecursiveCharacterTextSplitter

   text = "This is a very long text document that needs to be split into smaller chunks for easier processing."
   splitter = RecursiveCharacterTextSplitter(
       chunk_size=50,
       chunk_overlap=5,
       separators=["\n\n", "\n", ".", " "]
   )
   chunks = splitter.split_text(text)
   print(chunks)
   ```

   In this example, the text is split into chunks of up to 50 characters, with a 5-character overlap between chunks to maintain context. The splitter first tries to split by double newlines, then single newlines, periods, and finally spaces.

3. **Split by HTML Headers**
   - Designed to split HTML content by header tags (like `<h1>`, `<h2>`, etc.), making it useful for processing web pages.

   ```python
   from langchain_core.text_splitter import HTMLHeaderSplitter

   html_content = "<h1>Title</h1><p>Paragraph under title.</p><h2>Subtitle</h2><p>Another paragraph.</p>"
   splitter = HTMLHeaderSplitter()
   chunks = splitter.split_text(html_content)
   print(chunks)
   ```

4. **Split by HTML Sections**
   - Similar to splitting by headers, but focuses on HTML sections, which are useful for understanding page structure more broadly.

   ```python
   from langchain_core.text_splitter import HTMLSectionSplitter

   html_content = "<section>Section 1 content</section><section>Section 2 content</section>"
   splitter = HTMLSectionSplitter()
   chunks = splitter.split_text(html_content)
   print(chunks)
   ```

5. **Split by Character**
   - Splits text based on specific characters. It's a flexible method that can be tailored to various needs, like splitting by periods, commas, or newlines.

   ```python
   from langchain_core.text_splitter import CharacterTextSplitter

   text = "First sentence. Second sentence. Third sentence."
   splitter = CharacterTextSplitter(delimiter=".")
   chunks = splitter.split_text(text)
   print(chunks)
   ```

6. **Split Code**
   - This splitter is designed for code files, splitting them by functions or logical blocks, which is helpful for processing or analyzing code.

   ```python
   from langchain_core.text_splitter import CodeTextSplitter

   code = "def function1():\n    pass\ndef function2():\n    pass"
   splitter = CodeTextSplitter()
   chunks = splitter.split_text(code)
   print(chunks)
   ```

7. **Split Markdown by Headers**
   - Specifically for Markdown files, this splitter divides text by headers (`#`, `##`, etc.), which is useful for structured documents like README files or documentation.

   ```python
   from langchain_core.text_splitter import MarkdownHeaderSplitter

   markdown_content = "# Title\nContent under title.\n## Subtitle\nMore content."
   splitter = MarkdownHeaderSplitter()
   chunks = splitter.split_text(markdown_content)
   print(chunks)
   ```

8. **Recursively Split JSON**
   - This splitter breaks down JSON objects recursively, useful for large JSON files where you want to process or analyze parts of the data.

   ```python
   from langchain_core.text_splitter import JSONSplitter

   json_data = '{"key1": "value1", "key2": {"subkey1": "subvalue1", "subkey2": "subvalue2"}}'
   splitter = JSONSplitter()
   chunks = splitter.split_text(json_data)
   print(chunks)
   ```

9. **Split Text into Semantic Chunks**
   - This advanced splitter uses semantic meaning to divide text into chunks that make sense contextually, which is helpful for tasks like summarization or semantic search.

   ```python
   from langchain_core.text_splitter import SemanticTextSplitter

   text = "This is a long text that should be split into semantic chunks."
   splitter = SemanticTextSplitter()
   chunks = splitter.split_text(text)
   print(chunks)
   ```

10. **Split by Tokens**
   - Useful for splitting text by tokens, particularly when working with models that have token-based limitations (like GPT-3).

   ```python
   from langchain_core.text_splitter import TokenTextSplitter

   text = "Split this text based on tokens."
   splitter = TokenTextSplitter(max_tokens=10)
   chunks = splitter.split_text(text)
   print(chunks)
   ```

### Conclusion

Text splitters in LangChain are versatile tools that help break down large texts into manageable chunks tailored for different types of content. Depending on the application, you can choose the appropriate splitter to enhance text processing, search capabilities, or machine learning tasks.