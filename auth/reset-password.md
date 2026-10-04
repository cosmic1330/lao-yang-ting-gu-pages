---
layout: default
title: 重設密碼
lang: zh-TW
permalink: /auth/reset-password/
---

# 重設密碼

請按下方按鈕繼續驗證，完成後將自動開啟「老楊聽股」。

<p>
  <a id="continue-reset" href="#" rel="noreferrer noopener" style="display:none; padding:0.75rem 1.25rem; border-radius:0.5rem; background:#0f9d76; color:#fff; text-decoration:none; font-weight:700;">
    驗證並開啟 App
  </a>
</p>

<p id="invalid-reset" style="display:none; color:#b42318;">
  此重設連結不完整，請回到 App 重新申請。
</p>

<script>
(() => {
  const button = document.getElementById('continue-reset');
  const error = document.getElementById('invalid-reset');
  const marker = 'confirmation_url=';
  const markerIndex = window.location.search.indexOf(marker);

  try {
    if (markerIndex < 0) throw new Error('missing confirmation URL');

    // Keep the entire nested Supabase URL. This works whether the email
    // template URL-encodes ConfirmationURL or leaves its '&' characters raw.
    const encodedConfirmationUrl = window.location.search.slice(markerIndex + marker.length);
    const confirmationUrl = new URL(decodeURIComponent(encodedConfirmationUrl));

    if (
      confirmationUrl.origin !== 'https://zifjsqcvahkpytcklzed.supabase.co' ||
      confirmationUrl.pathname !== '/auth/v1/verify'
    ) {
      throw new Error('unexpected confirmation URL');
    }

    button.href = confirmationUrl.toString();
    button.style.display = 'inline-block';
  } catch {
    error.style.display = 'block';
  }
})();
</script>
