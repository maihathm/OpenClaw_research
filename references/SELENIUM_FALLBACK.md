# Selenium / Browser Fallback

## When to use browser automation

Escalate from normal fetch/search to browser automation only when:
- the page is JS-rendered and meaningful text does not appear in static fetches
- the content is hidden behind tabs, accordions, or lazy-loaded sections
- pagination or infinite scroll blocks simple extraction
- interaction is required to reveal version-specific docs, release notes, or article bodies

## Preferred order

1. Normal search
2. Static fetch
3. Browser automation fallback

## Extraction rules

- Use browser fallback narrowly, only for the blocked sources
- Extract text or links, not decorative page content
- Re-check the page after interaction before extracting
- Record that browser fallback was required
- If blocked by login, captcha, or unavailable dependencies, note the limitation and continue

## Local runtime prerequisites

Typical local requirements:
- Python
- Selenium Python package
- Chrome or Chromium
- ChromeDriver

Optional alternative:
- a browser automation CLI such as `agent-browser`

## Current environment checklist

At the time this repo was prepared, the local machine should verify these before relying on Selenium automation:
- `python --version`
- `python -c "import selenium"`
- `chromedriver --version`
- `agent-browser --version`

If any of these are unavailable, treat browser fallback as optional and non-blocking.
