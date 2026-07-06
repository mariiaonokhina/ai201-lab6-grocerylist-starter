# Code Review Notes

Fill this in as you work through the milestones. Each section mirrors the structure of a real GitHub pull request review.

---
## PR #1 — Bulk Purchase (`pr1_bulk_purchase.py`)

### Summary
*What does this PR do? (1–2 sentences in your own words)*

>It marks all items in a list as purchased.

### Issues

For each issue you find, note: where it is (file + function), what's wrong, and why it matters in production.

**Issue 1**
- Location: Lines 30 and 34
- What's wrong: The query filter returns all items even if purchased.
- Why it matters: If the items were marked purchased already, this would overwrite the status with a different user id.
- Suggested fix: Implement an "if" statement that checks whether an item was purchased before modifying the is_purchased status of an item.

**Issue 2**
- Location: Line 54
- What's wrong: The endpoint allows the user to omit user id in the request.
- Why it matters: If the user omits the user_id, it will be None, and the service will still mark all items as purchased by None.
- Suggested fix: Add an "if" statement. For example:
```python
if not user_id:
        return jsonify({"error": "Missing required field: user_id"}), 400
```

**Issue 3** *(if found)*
- Location: Line 37
- What's wrong: All items are counted and the number is returned to the user, even if they are unpurchased.
- Why it matters: This provides misinformation about the number of items that were actually marked as purchased.
- Suggested fix: Create a separate temporary list for the items that will be marked as purchased, then at the end, return the length of that list.

### Questions for the Author
*Things you're uncertain about — design choices that could be intentional or bugs depending on intent.*

>Did you mean to return the count of all items in the list after marking some of them as purchased OR should we return just the number of items that are being marked as purchased in this request?

### Verdict
- [ ] Approve — ship it
- [X] Request Changes — needs fixes before merging
- [ ] Comment — needs discussion before a verdict

**Rationale** *(1–2 sentences)*:

>The code has a couple of bugs that can unintentionally modify important data. It's better to fix them before implementing.

---

## PR #2 — List Stats (`pr2_list_stats.py`)

### Summary
*What does this PR do? (1–2 sentences in your own words)*

>

### Issues

**Issue 1**
- Location:
- What's wrong:
- Why it matters:
- Suggested fix:

**Issue 2**
- Location:
- What's wrong:
- Why it matters:
- Suggested fix:

**Issue 3** *(if found)*
- Location:
- What's wrong:
- Why it matters:
- Suggested fix:

### Questions for the Author
*A good code review often surfaces design questions, not just bugs. What would you want to clarify before approving?*

>

### Verdict
- [ ] Approve — ship it
- [ ] Request Changes — needs fixes before merging
- [ ] Comment — needs discussion before a verdict

**Rationale** *(1–2 sentences)*:

>

---

## Reflection

*Answer after completing both reviews.*

**1.** Which issue was hardest to spot, and why?

>

**2.** Which issues do you think an LLM reviewer (like Claude reviewing its own code) would most likely miss? Why?

>

**3.** One thing you'd add to a code review checklist for AI-generated backend code:

>
