---
name: mcpconf
description: Helps build out a conference agenda
license: Complete terms in LICENSE.txt
---

## Inputs

* **conference\_url** (optional): Conference homepage URL. Default: `https://mcpdevsummit.ai`

* **attendee\_goals** (required): What you want to accomplish at the conference.

* **attendee\_profile** (optional): Recommendation profile. Default: `technical builder / engineer`

* **priority\_topics** (optional): Topics to emphasize. Default: `infrastructure / hosting, orchestration / automation`

* **max\_vendors** (optional): Maximum number of vendors to recommend. Default: `8`

* **max\_sessions** (optional): Maximum number of sessions to recommend. Default: `5`

* **include\_related\_sessions** (optional): Whether to recommend sessions tied to top vendors or topics. Default: `yes`

## Steps

### 1. Load Conference Information

Using {{input.conference\_url}}, gather the current conference homepage plus any linked pages needed to identify sponsors, vendors, featured speakers, and the event schedule.

Capture:

* event dates and location

* sponsor and vendor organizations

* session titles, speakers, and descriptions if available

* any workshop, showcase, or expo information that helps identify vendor presence

If sponsor/vendor information cannot be found, stop and explain what is missing.

**On error:** stop

### 2. Build Vendor Candidate List

From the conference information, create a vendor candidate list focused on organizations that appear to offer MCP tooling, MCP infrastructure, hosting, orchestration, automation, observability, security, or related platform capabilities.

For each candidate, capture when available:

* company name

* sponsor tier or prominence

* apparent product/category fit

* evidence from the conference site that they are relevant

If fewer than 5 credible vendor candidates are found, stop and report the gap.

**On error:** stop

### 3. Score Vendors Against Attendee Priorities

Score each vendor candidate against:

* {{input.attendee\_goals}}

* {{input.attendee\_profile}}

* {{input.priority\_topics}}

Use explicit criteria:

* relevance to MCP tooling and platform needs

* strength in infrastructure / hosting

* strength in orchestration / automation

* technical depth likely available at the event

* uniqueness versus other vendors at the conference

* likely value of an in-person conversation

Return a ranked list of the top {{input.max\_vendors}} vendors with a concise explanation for each score.

### 4. Generate Meeting Strategy

For each recommended vendor, generate:

* why they are worth meeting

* the specific team or role to look for if inferable from the conference context

* 3 to 5 tailored technical questions to ask

* a suggested success criterion for the conversation

The questions should be concrete and technical, not generic marketing questions.

### 5. Identify Related Sessions

Identify the best sessions, speakers, workshops, or showcases to attend that reinforce the top vendor meetings or the attendee's priority topics.

Prioritize sessions that help the attendee:

* evaluate vendor claims

* understand implementation patterns

* compare platform approaches

* spot architectural tradeoffs

Return up to {{input.max\_sessions}} recommendations.

**Condition:** {{input.include\_related\_sessions}} equals yes

If no schedule or session detail is available and {{input.include\_related\_sessions}} equals yes, stop and explain what is missing.

**On error:** stop

### 6. Produce Final Recommendation

Produce a final recommendation with these sections:

* Attendee Objective Summary

* Top Vendors to Meet

* Why Each Vendor Made the List

* Suggested Questions by Vendor

* Best Sessions to Attend

* Gaps or Uncertainties

Be explicit about assumptions and cite conference evidence where possible.

## Output

# MCP Dev Summit Recommendation Brief

## Attendee Objective Summary

{{input.attendee\_goals}}

Profile: {{input.attendee\_profile}}
Topics: {{input.priority\_topics}}

## Top Vendors to Meet

{{Score Vendors Against Attendee Priorities}}

## Suggested Meeting Strategy

{{Generate Meeting Strategy}}

## Best Sessions to Attend

{{Identify Related Sessions}}

## Final Recommendation

{{Produce Final Recommendation}}

