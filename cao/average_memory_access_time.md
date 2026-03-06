# Average Memory Access Time (AMAT) — Review Note

---

## The Formula

$$AMAT = \text{Hit Time} + (\text{Miss Rate} \times \text{Miss Penalty})$$

---

## Key Terms

| Term | What it means |
|---|---|
| **Hit Time** | Time to check the cache + detect hit/miss (you ALWAYS pay this) |
| **Miss Rate** | Fraction of accesses that are NOT found in cache (e.g. 0.04 = 4%) |
| **Miss Penalty** | The **EXTRA** cycles paid on top of Hit Time when a miss occurs |
| **Clock Cycle Time** | Converts cycles → nanoseconds (e.g. 2ns/cycle) |

---

## What Happens on Every Access

```graphql
CPU requests data
       ↓
[Hit Time: 1 cycle] ← You ALWAYS pay this, no matter what
       ↓
  HIT? ✅                    MISS? ❌
       ↓                          ↓
   Done!                    Pay Miss Penalty
   Cost = 1 cycle           (extra 25 cycles)
                            Cost = 1 + 25 = 26 cycles
```

---

## Why Not (Hit Rate × Hit Time) + (Miss Rate × Full Miss Cost)?

Your intuition says: *"If miss rate is 20%, hit rate is 80% — shouldn't I weight both?"*

**You can! Both versions give the same answer.**

### Version 1 (Standard):
$$AMAT = \text{HT} + (\text{Miss Rate} \times \text{Miss Penalty})$$
$$= 1 + (0.2 \times 25) = 1 + 5 = \textbf{6 cycles}$$

### Version 2 (Your Intuition):
$$AMAT = (\text{Hit Rate} \times \text{HT}) + (\text{Miss Rate} \times \text{Full Miss Cost})$$
$$= (0.8 \times 1) + (0.2 \times 26) = 0.8 + 5.2 = \textbf{6 cycles}$$

### Same answer! Why?

Because **Hit Time is always paid** — even on a miss.
So it factors out completely:

$$= (0.8 \times 1) + (0.2 \times \underbrace{(1 + 25)}_{\text{HT + extra}})$$
$$= (0.8 \times 1) + (0.2 \times 1) + (0.2 \times 25)$$
$$= \underbrace{1 \times (0.8 + 0.2)}_{\text{= 1}} + (0.2 \times 25)$$
$$= 1 + (0.2 \times 25) \quad \leftarrow \text{Version 1!}$$

> **Key insight:** In Version 1, Miss Penalty = **extra cycles only**.
> In Version 2, Full Miss Cost = **Hit Time + extra cycles**.
> Don't mix them up!

---

## Worked Example

**Given:**
- Clock cycle time = 2ns
- Cache access time (including hit detection) = 1 cycle
- Miss rate = 0.04 misses/instruction
- Miss penalty = 25 clock cycles

**Step 1 — Convert to nanoseconds:**

| | Cycles | Time |
|---|---|---|
| Hit Time | 1 | 1 × 2ns = **2ns** |
| Miss Penalty | 25 | 25 × 2ns = **50ns** |

**Step 2 — Apply formula:**

$$AMAT = 2\text{ns} + (0.04 \times 50\text{ns})$$
$$= 2\text{ns} + 2\text{ns}$$
$$= \boxed{4\text{ns}}$$

---

## Intuition Check

> Without any misses → AMAT = **2ns** (just the hit time)
>
> With 4% miss rate → AMAT = **4ns** (doubled!)
>
> This shows how even a *small* miss rate has a big impact on performance.
> Halving the miss rate from 4% → 2% would save 1ns per instruction on average.

---

## Common Mistakes to Avoid

| Mistake | Correct thinking |
|---|---|
| Using full miss cost (26 cycles) in Version 1 | Version 1 uses **extra** penalty only (25 cycles) |
| Using extra penalty (25 cycles) in Version 2 | Version 2 uses **full** miss cost (26 cycles) |
| Forgetting to convert cycles → ns | Always multiply by clock cycle time |
