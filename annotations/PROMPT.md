# Coder instruction (identical for every coder)

Read the codebook in CODEBOOK.md. Then code every record in the items file you are given, in the given
order. Each line of the items file is a JSON object with keys id, title and abstract. Write one JSON
object per record to your output file, one per line, using the exact schema in the codebook and the
same id. Work only from the title and abstract. Do not open any other file in this folder except
CODEBOOK.md, your items file and your output file. Do not write code that assigns labels with keyword
rules: read and judge every abstract yourself. When finished, check that your output has one valid JSON
line per input record.
