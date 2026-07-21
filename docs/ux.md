# UX specification — the anti-widget

## The problem being rejected

Traditional assistant widgets fail the same way everywhere: a floating bubble that covers content, a modal that hijacks the page, an empty chat pane demanding the visitor compose a cold-start question, fake typing indicators, and a visual language imported from a vendor instead of the site. A4RON.AI does none of these.

## The interaction

**Resting state.** The existing A4RON.AI panel keeps its current design — status line, EQ bars, uptime. INITIALIZE CHAT is replaced by a terminal input line, always visible, always ready:

    > query the mainframe_

Zero clicks to begin. The blinking cursor is the invitation; nothing pops, nothing pulses for attention.

**Quick intents.** Three chips above the input for one-tap value: `PROJECTS` · `HIRE ME` · `WHAT IS THIS?` — each sends a real query and streams a real answer. Visitors who never type still get the demo.

**Response rendering.** Output streams into the panel styled as console output — timestamped, monospaced, in the sentinel-feed vocabulary. The conversation *is* terminal history. The panel grows to a capped height (~2× its resting size) then scrolls internally; the page never reflows around it.

**Honesty furniture.** A permanent one-liner under the input: `AI ASSISTANT · CAN BE WRONG · <a>REACH THE HUMAN</a>`. Every session's first response ends with the same signature. No pretending to be Aaron.

**Full-screen mode.** assistant.html is the same conversation with more room — same session, same visual language. A ⤢ glyph in the panel corner links to it. It is an expansion, not a different product.

**Voice (phase 3).** SPEAK activates push-to-talk: hold to speak, EQ bars animate on real audio, transcript renders in the same console stream. Mic state is always visible.

## Performance budgets

First token < 1.5s on the median; chips pre-warm nothing (no speculative spend). If the gateway is throttling or the budget cap is hit, the panel says so in-theme — `RATE LIMIT ENGAGED · TRY AGAIN SHORTLY` — never a spinner that lies.

## Failure states

Backend down: input line stays, submissions render `MAINFRAME UNREACHABLE · <a>contact Aaron directly</a>`. No dead ends: every failure path lands on a human contact route.
