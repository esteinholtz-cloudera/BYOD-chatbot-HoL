# Prerequisites for the lab “Bring your own data” LLM.

_The beauty of this lab is that you get to see an LLM at work with your own documents. The only limit for what you can do with this is your own imagination._ 

_The caveat is that you have to prepare these documents to be suitable for RAG (Retrieval-Augmented Generation)._

**Short version:** Documents have to be 

- in raw text format, 

- roughly 1kB, 

- however no bigger than 16kb size chunks.

**More verbose version:**

- Determine what process or problem you want to work with. Examples: 

  - Customer service solutions database. 

  - Legal texts that govern a process

  - Self-service how-to guides for customers

- If you are out of ideas, why not try a book from project Gutenberg (<https://www.gutenberg.org/>) ? Remember to use the .txt format though.

- Get a set of data that you want to query with the LLM. It has to be in raw text (.txt) format. Encoding/Character set: Preferably UTF-8. This means your Augmentation data can be in any language and character set supported by UTF-8. Note that both Embedders and LLMs (The two types of models we’ll be using in the lab) usually perform better on english due to the greater base of training material.

- When you have this base material, you need to chunk it into sections that are useful for the Embedding model to process. Useful chunk size typically means \~1000 bytes of size, That is roughly the same as half a page in a book.

  - The easiest way to chunk the data is to use “raw chopping”, ie just cut the text indiscriminately into a certain byte size. This is easily performed using the linux command line.

  - `split -b1k <file>`

  - To do it for a full directory of files, use for:

  - `mkdir split_temp;cd split_temp;for f in ../*.txt; do mkdir $f.dir; split -b1k $f; mv * $f.dir; done;cd ..`

  - This command sequence creates a temporary directory; then uses this directory as a base for the splitting files before moving them to a designated directory created per each source file.

- Advanced (and untested). If you’d like to get a better chopping of your files, line count can be useful. If your source material uses exactly one line per paragraph, this chunking can give a good result, as a paragraph is a good “semantic container”.

  - `split -l1 <file>`

  - Do check the size of your files afterwards. The limit of the LLM we will work with is 16kb.

Questions? Send them to [Erik Steinholtz](mailto:esteinholtz@cloudera.com), esteinholtz\@cloudera.com
