---
layout: default
title: Memes
description: "A browsable gallery of memes."
permalink: /memes/
body-class: memes
---

<p class="page-intro">Click to copy the link. ⌘-click (Ctrl on Windows) to open the full image in a new tab.</p>
<p class="copy-hint" id="copyHint" hidden>Copied!</p>
<p class="meme-hint"><a class="add-meme" href="https://github.com/nicgrayson/nicgrayson.github.io/compare/main...main?expand=1&template=add_meme" target="_blank" rel="noopener">＋ Add a meme</a></p>

<div class="meme-gallery">
{% for img in site.data.images.images %}
  <a class="meme" href="/images/{{ img.name }}" title="{{ img.name }}" data-url="/images/{{ img.name }}" target="_blank" rel="noopener">
    <img src="/images/{{ img.name }}" alt="{{ img.name }}" loading="lazy">
    <span class="meme-name">{{ img.name }}</span>
  </a>
{% endfor %}
</div>

<script>
(function () {
  var gallery = document.querySelector('.meme-gallery');
  var hint = document.getElementById('copyHint');

  function copy(text) {
    if (navigator.clipboard && window.isSecureContext) {
      return navigator.clipboard.writeText(text);
    }
    var ta = document.createElement('textarea');
    ta.value = text;
    ta.style.position = 'fixed';
    ta.style.opacity = '0';
    document.body.appendChild(ta);
    ta.select();
    var ok = false;
    try { ok = document.execCommand('copy'); } catch (e) {}
    document.body.removeChild(ta);
    return ok ? Promise.resolve() : Promise.reject();
  }

  gallery.addEventListener('click', function (e) {
    var link = e.target.closest('.meme');
    if (!link) return;

    // Cmd/Ctrl-click or middle-click: let the browser open the image in a new tab.
    if (e.metaKey || e.ctrlKey || e.button === 1) {
      return;
    }

    e.preventDefault();
    var url = link.getAttribute('href');
    var absolute = new URL(url, window.location.origin).href;
    copy(absolute).then(function () {
      hint.hidden = false;
      hint.classList.add('show');
      setTimeout(function () {
        hint.classList.remove('show');
        setTimeout(function () { hint.hidden = true; }, 300);
      }, 1200);
    }).catch(function () {
      window.alert('Could not copy: ' + url);
    });
  });
})();
</script>