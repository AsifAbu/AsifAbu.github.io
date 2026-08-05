# Certificate files - drop one in, a "View certificate" link appears

Credentials on this site are **link-only by design**. Nothing is embedded as an image;
the visitor clicks through to view the certificate. That keeps every card the same
shape and sends people to the issuer's own page wherever one exists.

Each credential card in `index-v2.html` carries `data-cert="<slug>"`. On load the page
sends a `HEAD` request for `assets/certs/<slug>.pdf`, then `.png`, then `.jpg`. The
**first one that returns 200** adds a `View certificate ↗` link to that card. No HTML
editing needed, and a miss costs one bodyless request.

## Slugs

| Credential | Slug | Verify link currently live |
|---|---|---|
| ISTQB CTFL v4.0 | `istqb` | ISTQB registry + official iSQI badge |
| SQA Capture the Flag 2026 | `ctf` | certificate page (cert ID `SQACTF26-193385`) |
| HIPAA | `hipaa` | none - internal training, no public registry |
| Ready for SAFe® | `safe` | Credly badge |
| Generative AI for Everyone | `genai` | none yet |

PDF is the best format to drop here - it stays sharp and is what a recruiter expects to
open. An image works too; around 1600px on the long edge is plenty.

## Optional - these already have issuer links

`istqb`, `ctf` and `safe` all point at the issuing body already, so adding a local file
for them is optional and will produce a *second* link on the card. Only add one if you
want visitors to be able to view the certificate without leaving the site.

The two worth adding are the ones with no public registry at all:

- `hipaa.pdf` - the training completion certificate
- `genai.pdf` - plus a public credential URL if the course issues one (Coursera and
  DeepLearning.AI both do; send it and it becomes a proper issuer link instead)

## What was never reachable

**LinkedIn.** It returns HTTP 999 to automated requests and no Chrome extension was
connected to the session across repeated attempts, so the certification section - and
the images attached there - could not be read. Both URLs now wired (CTF and Credly)
were supplied directly.

**The CTF certificate graphic.** `sqa-ctf-2026-results.hurayraiit.com` returns **403 to
every automated client**, browser user-agent included, and the preview browser is
sandboxed to localhost. The link works fine for a human. To host the graphic locally,
open the certificate, save the image, and drop it here as `ctf.png`.
