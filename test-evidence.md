# Beyond live-research validation notes

Date: 2026-10-17. These are provider-returned discovery records from development tests. Destination pages were not independently crawled or verified; the URLs below are real returned links, not claims of full-page inspection.

## Discovery calibration

An early Tavily run for “Build an AI tool that helps students prepare for exams” returned editorial records rather than comparable products:

- Yahoo Finance, “CamScanner Introduces Solver AI to Bring Students Advanced Learning Tools for Finals Week”: https://finance.yahoo.com/news/camscanner-introduces-solver-ai-bring-130000061.html
- Vertech Academy, “7 Best AI Exam Prep Tools for Students [Ranked for 2026]”: https://www.vertechacademy.com/blog/best-ai-exam-prep-tools

The pipeline was tightened to count news, roundups, listicles, and editorial pages as discoveries but exclude them from comparable-product cards and disclose those exclusions.

An early repository-only run against https://github.com/fastapi/fastapi returned these metadata/snippet candidates:

- GraphBit Python documentation: https://docs.graphbit.ai/python
- public-apis/public-apis repository: https://github.com/public-apis/public-apis

The directory was subsequently excluded as a comparable project. Documentation and broad technical-topic matches are not treated as equivalent products.

## Verified flows

The latest streamed idea-only test used “Build an AI tool that helps students prepare for exams.” It completed in 32.6 seconds with all six real stages in order: understanding, GitHub, web, comparing, evidence, and opportunities. The source-tagged profile event arrived before GitHub discovery. GitHub, Tavily, and AI were available; 25 records were discovered, five repositories were inspected, six editorial records and five weak matches were disclosed as excluded, and three opportunity directions were returned. This bounded run passed two GitHub comparables through the same-problem/workflow gate:

- Savsoft Quiz, described by the returned repository evidence as an online quiz/exam creation and delivery system: https://github.com/savsofts/savsoftquiz_v4.0_advance
- Online Examination System, described by its returned repository evidence as objective exam delivery and student assessment: https://github.com/projectworldsofficial/online-examination-systen-in-php

A separate repository-only run against https://github.com/fastapi/fastapi built a REPOSITORY-OBSERVED project name/technology profile plus an AI-INFERRED problem profile. Six repository records were inspected and three opportunity hypotheses were returned. No candidate met the same-problem/workflow relevance gate, so the shortlist stayed empty rather than promoting broad technical or index matches.

Mixed idea-plus-repository input, invalid GitHub URL rejection, provider health, and the route manifest were also exercised. Invalid repository URLs receive a validation error before provider requests. An externally forced provider outage was not simulated; provider failures, bounded response bodies, named coverage notes, partial results, and retry controls are implemented in the application.

These tests are illustrative, not exhaustive market research. Search snippets and repository READMEs remain unverified source material, and an empty shortlist is not evidence that no comparable project exists.
