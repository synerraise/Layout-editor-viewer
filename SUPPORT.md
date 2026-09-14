# Layout AI Agent Support Policy

## Supported product

Support applies to unmodified Layout AI Agent packages distributed through an
official release channel. The current product is an Early Access GDSII viewer
and basic editor, not a signoff verification tool. The supported and excluded
workflows are listed in `README.md` and in **Help > Release Scope & Safe
Workflow**.

## What to include in a report

Provide:

- the application version from **Help > About**;
- operating system, architecture, and display scaling;
- exact steps, expected result, and observed result;
- whether the issue reproduces with a small non-confidential layout;
- relevant files from `logs/`, when disclosure is permitted; and
- the GDS generator and foundry/technology family when relevant and permitted.

Do not submit proprietary GDS, native projects, screenshots, logs, or foundry
material without authorization from the data owner. A minimal synthetic
reproducer is preferred.

## Severity

- **Critical:** data loss/corruption, security exposure, or inability to open a
  previously supported native document.
- **High:** a supported workflow is blocked with no practical workaround.
- **Normal:** incorrect or degraded behavior with a workaround.
- **Low:** cosmetic issue, documentation issue, or feature request.

Response and resolution times are contractual only when stated in a separate
customer agreement. Public repository activity is not an SLA.

## Diagnostic retention

Layout AI Agent writes local diagnostics under `logs/` and crash diagnostics
under `target/` in development builds. Review files before sharing them. The
application does not automatically upload customer layout data or diagnostics.

