# Working conventions

This is a personal, growing reference. These rules keep it consistent as it grows.

## Adding content

1. Put the file in the right folder: `templates/`, `best-practices/`, `cheatsheets/`, `detection/`, `learning/`.
2. Use lowercase file names with hyphens and no spaces (`playbook-ransomware.md`).
3. Write original content. Link to sources instead of copying copyrighted documents; cite and attribute anything adapted.
4. Add a "Last reviewed" or date marker to templates and playbooks, and a **Standards** line to best-practice pages.
5. Add the file to the index table in [README.md](README.md).
6. Check that your links work and the README index lists the new file.
7. Add a line to [learning/log.md](learning/log.md).

## Quality bar

- Accurate and specific: say what to do and why.
- Safe: never include real credentials, customer data, or live indicators from real incidents. Defang indicators.
- Honest: mark content as `experimental` or "indicative" if it has not been validated.

## Commits

Small and frequent, with a clear message (`Add Linux auditd Sigma rules`, `Fix link in IR plan`).

## Responsible use

Everything here is for defensive use and education. Test techniques only on systems you own or are authorised to test.
