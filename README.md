# sticky-beak
Automated LLM Wiki

WIP - built & working but not fully tested. to share soon

-outdated readme- more functionality & speed added in the past days

Pipeline Execution Sequence
The pipeline is designed as a sequential ETL process. Each script depends on the state mutations performed by the previous one. The required execution order is:

#1 
*sync_wiki.sh*: The extraction layer. It queries the GitHub API for state changes, clones missing repositories, and flattens them into markdown via repomix.

#2 
*tagger.py*: The classification layer. It processes un-categorized markdown files and uses local LLM inference to assign the taxonomy (category, sub_category).

#3
*sticky_beak.py*: The data enrichment layer. It performs asynchronous network requests (Reddit, GitHub metrics) to calculate and inject the vitality_score into the frontmatter.

#4
*curator.py*: The deduplication layer. It groups repositories by sub-category and relies on the pre-calculated vitality_score to instruct the LLM on which overlapping tools to deprecate.

#5
*synthesizer.py*: The compilation layer. It reads the final state of active repositories and generates the _Overview_ architecture documents for each domain.
