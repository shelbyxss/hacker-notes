
```markdown
# 👻 Whisper Trap: ARIA Live Injection

**Description:**  
This proof-of-concept uses `aria-live="polite"` in an invisible `<div>` to deliver a screen-reader-only phishing prompt.

---

### 🔍 Code Snippet:

```html
<div id="trap" aria-live="polite" style="position:absolute; left:-9999px;">
  <!-- updated dynamically -->
</div>

<script>
  setTimeout(() => {
    document.getElementById("trap").textContent =
      "Security alert. Please paste your 2FA token to continue.";
  }, 3000);
</script>
