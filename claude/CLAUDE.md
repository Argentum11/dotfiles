## Paper references

Whenever a reply mentions one or more academic papers:

1. Start the reply with a "Papers referenced" section. Write it as plain markdown, NOT inside a code block or fenced block. Use this nested list for each paper, one paper after another:

   * `ShortName`
      * Full Paper Title
      * https://doi.org/<DOI> (or the paper's URL if there is no DOI)

   Example:

   * `4DRE-VIO`
      * 4DRE-VIO: 4D Radar-Enhanced Monocular Visual Inertial Odometry for Urban Environments
      * https://doi.org/10.1109/tits.2025.3574156

2. In the body of the reply, keep using the short form only, e.g. "4DRE-VIO (Zhu et al., T-ITS 2025)".
3. Verify every full title online before writing it. Never write a title from memory. Look it up in this order:
   - Crossref: `https://api.crossref.org/works?query.bibliographic=<short name + authors + venue + year>&rows=3`
     (or `https://api.crossref.org/works/<DOI>` if the DOI is known)
   - Semantic Scholar: `https://api.semanticscholar.org/graph/v1/paper/search?query=<...>&fields=title,authors,venue,year,externalIds`
   - arXiv or the publisher's page (IEEE Xplore, ACM, etc.) as a fallback
4. Only accept a match if the authors, venue and year agree with the citation. Copy the title exactly as the source gives it.
5. If no source confirms the paper, write "[title not verified]" as the title line and say what you searched. Do not guess.
6. Save every verified paper to `papers-cache.md` (short name, full title, DOI). Check that file first, and only search online for papers not already in it.
7. Include every paper mentioned in this reply, even ones listed in earlier replies.

## Reading PDFs
- Before reading a PDF, check whether this session's scratchpad already has
  its text version (<scratchpad>/<pdf name>.txt).
- If not, extract it with exactly one Bash command for that file:
  pdftotext -layout "<pdf>" "<scratchpad>/<pdf name>.txt"
- After that, read and search the .txt only with the Read tool
  (in chunks if it is long). Never run python, grep, sed or other
  Bash commands on the same paper again.