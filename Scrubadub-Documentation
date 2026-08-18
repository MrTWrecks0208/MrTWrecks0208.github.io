# Scrubadub End-User Documentation

<details open>
  
<summary>🔍 Overview</summary> 
**Scrubadub** is a real-time multi-string match and replace ("scrub") tool which allows you to create any number of rules using regular expressions, strings, and/or patterns to find and replace as many strings or patterns as needed within a large body of text.

### Key Principles
- **Sequential Execution**: Rules run from top to bottom. Each rule operates on the transformed output of the rule that preceded it.
- **Real-Time Visual Validation**: Text matching your active regular expressions is highlighted live in the source viewer with high-contrast indicator bands before changes are finalized.
- **AI-Assisted Rule Synthesis**: Describe what you want to extract or redact in natural language, and the integrated Gemini AI will generate, validate, and explain the regex pattern for you.
- **Client-Side Privacy First**: All pattern matching, replacements, and data processing happen entirely within your local browser runtime. Your text is never transmitted to an external server for processing, monetization, or advertising.

</details>

<details>
  
<summary>📐 Layout</summary>

The Scrubadub workspace is organized into two primary columns below the top header and preset bar:

```
┌──────────────────────────────────────────────────────────────────────────────────┐
│  HEADER: Logo                                                  Auth / Account    │
|  Rule Sets                                                                       |
├─────────────────────────────────────────┬────────────────────────────────────────┤
│  LEFT COLUMN (Editor Panels)            │  RIGHT COLUMN (Rules Management)       │
│                                         │                                        │
│  1. Source Input (Top)                  │  1. AI Rule Generator                  │
│     - Raw text editor                   │     - Prompt-to-regex generator        │
│     - Live match highlighting overlay   │                                        │
│     - Generate Sample Data & Clear      │  2. Rules List                         │
│                                         │     - Add Rule & Save Rule Set actions │
│  2. Scrubbed Output (Bottom)            │     - Ordered regex rules cards        │
│     - Real-time sanitized result        │     - Renaming, Patterns, Flags,       │
│     - Copy & Download actions           │       Replace With, & Enable/Disable   │
│     - Matches & character stats         │                                        │
└─────────────────────────────────────────┴────────────────────────────────────────┘
```

**Header (Logo, Account, and Rule Sets)**
   - Quick-switch selector for built-in rule sets (*PII Redactor*, *HTML Stripper*, *Log Cleaner*, *Code Minifier*).
   - Custom rule sets bar to load or delete your saved custom rule sets.
   - User account & authentication menu.

**Left Column (Editor Panels)**
   - **Source Input (Top Left)**: Enter or paste your raw text. Live color-coded overlays highlight all matched regions directly under your text cursor. Includes a sample data generator and clear button.
   - **Scrubbed Output (Bottom Left)**: Displays the live sanitized result right below the source input, complete with one-click clipboard copy, plain-text download, and real-time match/alteration statistics.

**Right Column (Rules Management)**
   - **AI Rule Generator (Top Right)**: Describe matching patterns in plain English to automatically synthesize rules.
   - **Rules List (Bottom Right)**: Add rules, reorder them, adjust regex patterns and replacements, toggle flags (`g`, `i`, `m`, `s`), enable/disable rules, and save your rules into custom rule sets.
     
</details>

<details>
  
<summary>📋 Getting Started</summary>

## Source Input
  The **Source Input** pane is on the left-hand side of the screen. Paste your text into the Source Input.
  The engine operates on an ordered list of rules. When text is entered into the Source Input, it passes through Rule 1. The resulting text is then fed directly into Rule 2 and so on through the end of your active rules.

### Matched Regions
- As you enter, paste, or edit text in the Source Input, Scrubadub highlights every matched text segment in real time.
- Matches from active rules are rendered with distinct visual highlight boxes synchronized behind the text cursor, allowing you to verify exactly what will be modified before you export your data.

### Generate Sample Data
- To test rules immediately without exposing real customer data or searching for test files, click the **`Generate Sample Data`** button above the source editor.
- Scrubadub automatically injects structured test data tailored to your active rules (including realistic mock emails, phone numbers, IP addresses, JSON objects, or server logs).

## Rules & Rule Sets

### Creating Rules
- Click the **`+ Add Rule`** button in the Rules panel to append a new blank rule.
- You can create as many rules as needed to handle distinct patterns independently.
- Alternatively, clicking any **Built-in Rule Set** in the top bar will populate your workspace with a curated set of rules tailored to that specific domain.

### Renaming Rules
- Click directly on the rule name field (e.g., `Rule 1`, `Rule 2`) to assign a meaningful label, such as *"Redact SSNs"*, *"Strip <script> tags"*, or *"Mask IPv4 Addresses"*.
- Naming rules makes multi-step cleaning easy to inspect, debug, and maintain.

### Patterns

#### Regular Expressions
- In the **Pattern** input field, type standard ECMAScript / JavaScript regular expression syntax (without enclosing forward slashes `/`).
- **Examples**:
  - `\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b` (Email addresses)
  - `\b\d{3}-\d{2}-\d{4}\b` (US Social Security Numbers)
  - `(?:\d{1,3}\.){3}\d{1,3}` (IPv4 Addresses)
  - `<[^>]+>` (HTML tags)
- **Live Syntax Validation**: If your regex contains an invalid token or an unclosed group, an error indicator will immediately alert you without interrupting your session.

#### AI Rule Generator
- If you don't know the exact regex syntax or are dealing with complex edge cases:
  1. Click the **`AI Assistant`** / **`Generate with AI`** button in the header or rule section.
  2. Enter a natural language description of what you want to match, such as:
     - *"Match Canadian postal codes like A1A 1A1"*
     - *"Find all UUID v4 strings"*
     - *"Match ISO 8601 formatted timestamps (YYYY-MM-DDTHH:MM:SSZ)"*
     - *"Extract dollar amounts like $1,250.00"*
  3. The Gemini AI synthesizes the regular expression, provides a step-by-step breakdown of how the tokens work, and inserts the completed rule into your rules list with recommended flags.

### Replace With
- In the **Replace With** field, enter the replacement string that will substitute for each matched occurrence.
- **Blank / Empty (Default)**: If left blank, matched text will simply be removed from the final output.
- **Literal Text Replacement**: Enter literal placeholder strings such as `[REDACTED]`, `***`, `HIDDEN`, or `0.0.0.0`.
- **Capture Groups & Backreferences**: You can use standard regex replacement tokens to rearrange or preserve parts of the matched text:
  - `$1`, `$2`, `$3`: References capture groups `(...)` defined in your pattern.
  - `$&`: Inserts the entire matched substring.
  - *Example*: Pattern `(\w+)\s(\w+)` with Replace With `$2, $1` transforms `"John Doe"` into `"Doe, John"`.

### Flags
Each rule includes toggleable flag pills that alter regular expression engine behavior:
- **`g` (Global Match)**: Finds all matches across the entire text rather than stopping after the first occurrence. (Recommended for scrubbing).
- **`i` (Case Insensitive)**: Ignores character casing so that `[a-z]` matches uppercase letters as well.
- **`m` (Multiline Mode)**: Treats the beginning (`^`) and end (`$`) assertions as matching the start and end of each individual line, rather than the start and end of the entire input string.
- **`s` (DotAll / Single Line)**: Allows the dot `.` wildcard to match newline characters (`\n`), enabling matches that span across multiple lines.

### Enable/Disable
- Every rule card includes an **Active Toggle switch**.
- You can turn individual rules off temporarily to test how the rest of your rules behave, without having to delete the rule or lose its configuration.

### Saving Rules
Scrubadub requires an account in order to save custom rule sets. Please refer to the section below, "Rule Sets", for more information. 

</details>

<details>

<summary>🧰 Rule Sets</summary>
  
### Understanding Rule Sets
<strong>_Note: You <span style="text-decoration-line: underline;text-decoration-style: solid;text-decoration-thickness: 1.5px">MUST</span> create an account in order to create and save custom rule sets and sync them across all of your devices._</strong>

- Once you have configured and tested your rules, you can bundle them into a permanent **Rule Set**.
- Click the **`Save Rule Set`** button in the top action bar or rules header.
- Provide a name (e.g., *"Kubernetes Log Sanitizer"*) and an optional description.
- Your saved rule sets will appear in the **Custom Rule Sets** bar at the top for one-click loading on any device where you are signed in.
- You can manage, update, or delete existing custom rule sets from the custom rule sets bar.
  
</details>

<details>
  
<summary>🧼 Scrubbed Output</summary>

The **Scrubbed Output** pane is on the bottom left-hand side of the screen below the Source Input pane. The Scrubbed Output pane displays the real-time result produced by executing your active rules against the source text.

### Copy
- Click the **`Copy`** button in the output panel header to copy the entire scrubbed text directly to your clipboard.
- A visual checkmark confirmation verifies that the text was copied successfully.

### Download
- Click the **`Download`** button to export the scrubbed output as a clean `.txt` plain-text file to your local computer.

### Stats
The telemetry toolbar at the top of the output panel displays real-time execution analytics:
- **Matches Found**: The total count of all matched text instances across all active rules.
- **Characters Altered / Removed**: The net difference in character count between the raw input and the final scrubbed output.
- **Line & Word Counts**: Total line and word counts for the sanitized document.
- **Execution Time**: The time in milliseconds (ms) taken to execute your rules, ensuring high-throughput performance.

</details>

<details>
  
<summary>📚 Additional Resources</summary>

### RegEx Cheat Sheet

For testing complex patterns, inspecting detailed regex token trees, and debugging regular expressions, visit [regex101.com](https://regex101.com).

### Quick Reference Table

| Category | Token | Description | Example |
| :--- | :--- | :--- | :--- |
| **Character Classes** | `.` | Any single character except newline | `c.t` matches `cat`, `c0t` |
| | `\d` | Any digit `[0-9]` | `\d{3}` matches `555` |
| | `\D` | Any non-digit character `[^0-9]` | `\D+` matches `abc` |
| | `\w` | Word character `[a-zA-Z0-9_]` | `\w+` matches `user_1` |
| | `\W` | Non-word character | `\W` matches `!`, `@`, `#` |
| | `\s` | Whitespace (spaces, tabs, newlines) | `\s+` matches `   ` |
| | `\S` | Non-whitespace character | `\S+` matches non-empty text |
| **Anchors & Boundaries** | `\b` | Word boundary | `\bcat\b` matches `cat`, not `scat` |
| | `\B` | Non-word boundary | `\Bcat` matches `scat` |
| | `^` | Beginning of string (or line with `m` flag) | `^Error` |
| | `$` | End of string (or line with `m` flag) | `done$` |
| **Quantifiers** | `*` | 0 or more occurrences (greedy) | `ba*` matches `b`, `ba`, `baaa` |
| | `+` | 1 or more occurrences (greedy) | `ba+` matches `ba`, `baaa` |
| | `?` | 0 or 1 occurrence (optional) | `https?` matches `http`, `https` |
| | `{n}` | Exactly `n` occurrences | `\d{4}` matches `2026` |
| | `{n,m}` | Between `n` and `m` occurrences | `\d{2,4}` matches `12`, `123`, `1234` |
| | `*?`, `+?` | Lazy / Non-greedy quantifiers | `<.+?>` matches `<p>` in `<p>text</p>` |
| **Groups & Lookarounds** | `(...)` | Capturing group (reference with `$1`) | `(\d{3})-(\d{4})` |
| | `(?:...)` | Non-capturing group | `(?:https?\|ftp)://` |
| | `(?=...)` | Positive Lookahead (followed by) | `\d+(?=px)` matches `10` in `10px` |
| | `(?!...)` | Negative Lookahead (not followed by) | `\d+(?!px)` matches `10` in `10em` |
| | `(?<=...)` | Positive Lookbehind (preceded by) | `(?<=\$)\d+` matches `100` in `$100` |
| | `(?<!...)` | Negative Lookbehind (not preceded by)| `(?<!\$)\d+` matches `100` in `€100` |

</details>
