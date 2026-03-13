title: Cross Scanner Skill
description: AI-powered scanner for writing tasks
version: 1.0.0
tags: writing, ai, automation
author: SMOUJ
date: 2026-03-13
---

# Cross Scanner Skill

## Purpose

The Cross Scanner is an advanced AI-powered tool integrated into OpenClaw, specifically designed for analyzing and enhancing written content across various domains. It leverages natural language processing and machine learning models to provide comprehensive feedback on writing quality, including grammar corrections, style improvements, readability enhancements, and content optimization suggestions.

### Real Use Cases

- **Blog Content Optimization**: Scanning blog posts for SEO keywords, readability scores (using Flesch-Kincaid), and engagement metrics to improve online visibility and user retention.
- **Technical Documentation Review**: Analyzing API docs, user manuals, or code comments for clarity, consistency, and technical accuracy, ensuring they meet industry standards like ISO/IEC 18004.
- **Creative Writing Enhancement**: Reviewing novels, short stories, or scripts for narrative flow, character development, plot coherence, and stylistic elements like metaphor usage and pacing.
- **Professional Communication Audit**: Proofreading business emails, reports, or presentations for tone appropriateness, bias detection, and cultural sensitivity to maintain corporate image.
- **Academic Paper Analysis**: Evaluating research papers for citation integrity, argument strength, and adherence to academic writing conventions (APA, MLA, Chicago styles).
- **Marketing Copy Refinement**: Optimizing ad copy, product descriptions, or social media posts for persuasive language, call-to-action effectiveness, and audience targeting.

## Scope

### Specific Commands

The Cross Scanner operates through a set of CLI commands accessible via OpenClaw's interface:

- `openclaw cross-scanner scan-text --input "text here" --mode grammar`: Scans provided text for grammatical errors and basic corrections.
- `openclaw cross-scanner scan-file --path /path/to/file.md --output report.json`: Analyzes a file and generates a detailed JSON report.
- `openclaw cross-scanner suggest-improvements --content "text" --focus readability`: Provides targeted suggestions for improving specific aspects like readability or SEO.
- `openclaw cross-scanner generate-summary --file /path/to/document.txt --length short`: Creates a concise summary of the scanned content.
- `openclaw cross-scanner compare-versions --original file1.txt --revised file2.txt`: Compares two versions of text and highlights differences with improvement scores.
- `openclaw cross-scanner batch-scan --directory /path/to/folder --filter "*.md"`: Processes multiple files in a directory with wildcard filtering.

### Environment Variables

- `CROSS_SCANNER_API_KEY`: Required API key for accessing AI models (e.g., OpenAI GPT-4 or similar). Set via `export CROSS_SCANNER_API_KEY=your_key_here`.
- `CROSS_SCANNER_MODEL`: Optional model selection (default: "gpt-4"). Options include "claude-3" or "llama-3".
- `CROSS_SCANNER_TIMEOUT`: Maximum processing time in seconds (default: 30).
- `CROSS_SCANNER_LANGUAGE`: Target language for analysis (default: "en"). Supports ISO language codes like "es" for Spanish.

### Dependencies and Requirements

- **System Requirements**: Linux/macOS/Windows with Python 3.8+, Node.js 16+ for integration.
- **Dependencies**: Install via `pip install openai langchain nltk spacy`. Requires `spacy` models: `python -m spacy download en_core_web_sm`.
- **API Access**: Valid subscription to supported AI providers (OpenAI, Anthropic, or local models via Ollama).
- **Storage**: Minimum 1GB free disk space for temporary reports and cached analyses.

## Detailed Work Process

1. **Input Validation**: Verify input text/file exists and meets size limits (max 10MB per file, 50,000 characters for direct text).
2. **Preprocessing**: Tokenize text using NLTK, detect language with langdetect, and apply basic filtering for noise reduction.
3. **AI Analysis**: Send processed content to selected AI model with specific prompts (e.g., "Analyze this blog post for SEO and suggest improvements").
4. **Feedback Generation**: Receive model response, parse into categories (grammar, style, content, SEO), and score each aspect on a 0-100 scale.
5. **Output Formatting**: Generate human-readable report with inline suggestions, colored highlights (red for errors, yellow for warnings, green for positives), and export options (JSON, Markdown, PDF).
6. **User Interaction**: Allow interactive mode where users can accept/reject suggestions via CLI prompts.
7. **Logging and Metrics**: Record analysis time, token usage, and accuracy metrics for continuous improvement.

### Verification Steps

- **Post-Scan Check**: Run `openclaw cross-scanner verify --report report.json` to validate report integrity and cross-reference with original content.
- **Accuracy Test**: Compare AI suggestions against manual proofreading for a sample set; aim for >85% agreement.
- **Performance Benchmark**: Ensure average scan time <5 seconds for <1000 words using `time openclaw cross-scanner scan-text --input "sample text"`.
- **Integration Test**: Confirm output integrates with OpenClaw's file editor without conflicts.

## Golden Rules

1. **Preserve Authenticity**: Never alter the core message or author's unique voice; suggestions should enhance, not replace.
2. **Ethical AI Use**: Avoid biased suggestions; use diverse training data and implement fairness checks.
3. **Privacy First**: Process content locally when possible; never transmit sensitive data without explicit consent.
4. **Actionable Feedback**: Every suggestion must include why it's recommended and how to implement it.
5. **Context Awareness**: Adapt analysis based on content type (e.g., formal for reports, creative for fiction).
6. **Continuous Learning**: Incorporate user feedback to refine AI prompts and improve future scans.
7. **Resource Efficiency**: Limit API calls to prevent overuse; cache frequent analyses for repeated content.

## Examples

### Example 1: Basic Grammar Scan
**Input Command**: `openclaw cross-scanner scan-text --input "This is a example sentance with to many erros."`

**Output**:
```
Scanning complete in 2.3 seconds.

Original: "This is a example sentance with to many erros."
Corrected: "This is an example sentence with too many errors."

Suggestions:
- Grammar: Changed "a" to "an" (indefinite article rule).
- Spelling: "sentance" → "sentence", "erros" → "errors".
- Style: "to many" → "too many" (quantifier correction).

Score: Grammar: 75/100 | Readability: 82/100
```

### Example 2: File Analysis with SEO Focus
**Input Command**: `openclaw cross-scanner scan-file --path /home/user/blog-post.md --focus seo --output seo-report.json`

**Output** (excerpt):
```
File: /home/user/blog-post.md (1245 words)

SEO Analysis:
- Keyword Density: "machine learning" appears 8 times (optimal range: 1-2%).
- Meta Description: Missing; Suggestion: "Explore the latest in machine learning techniques for data scientists."
- Readability: Flesch Score: 68 (aim for 60-70).
- Suggestions: Add internal links to related posts, optimize H1/H2 tags.

Full report saved to seo-report.json.
```

### Example 3: Creative Writing Review
**Input Command**: `openclaw cross-scanner suggest-improvements --content "The hero walked slowly into the dark forest, his heart pounding." --mode creative`

**Output**:
```
Creative Enhancements:
- Sensory Detail: Add descriptions (e.g., "The crunch of leaves underfoot echoed his pounding heart").
- Pacing: Consider breaking into shorter sentences for tension.
- Metaphor: "His heart pounded like a war drum" could heighten drama.

Overall Tone: Suspenseful, but could be more immersive.
```

## Rollback Commands

- **Undo Single Change**: `openclaw cross-scanner undo --report report.json --change-id 3` (reverts specific suggestion by ID).
- **Revert File**: `openclaw cross-scanner revert-file --original /path/to/original.txt --modified /path/to/modified.txt` (overwrites modified with original).
- **Clear Cache**: `openclaw cross-scanner clear-cache` (removes all cached analyses to start fresh).
- **Reset Session**: `openclaw cross-scanner reset` (clears current session data and preferences).

## Troubleshooting

### Common Issues
- **API Rate Limit**: Error "429 Too Many Requests". Solution: Increase `CROSS_SCANNER_TIMEOUT` or switch to a different model.
- **Large File Error**: "File exceeds size limit". Solution: Split file into chunks using `split -l 1000 file.txt chunk_` then batch scan.
- **Language Detection Failure**: Output shows "Unknown Language". Solution: Manually set `CROSS_SCANNER_LANGUAGE=es` for non-English content.
- **Inaccurate Suggestions**: Low scores in verification. Solution: Update AI model via `pip install --upgrade openai` or switch providers.
- **Timeout Errors**: Process hangs. Solution: Reduce content length or increase timeout; check network connectivity.

### Logs and Debugging
- Enable verbose mode: Add `--verbose` flag to any command.
- Check logs: `tail -f /home/smouj/.openclaw/logs/cross-scanner.log`
- Report bugs: Use `openclaw feedback --skill cross-scanner --issue "description"` to submit to developers.