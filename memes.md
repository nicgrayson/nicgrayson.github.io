---
layout: default
title: Memes
description: "A browsable gallery of memes."
permalink: /memes/
---

<p class="page-intro">Click any image to copy its link.</p>
<p class="copy-hint" id="copyHint" hidden>Copied!</p>

<div class="meme-gallery">
{% for img in site.data.images.images %}
  <a class="meme" href="/images/{{ img.name }}" title="{{ img.name }}" data-url="/images/{{ img.name }}">
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
    e.preventDefault();
    var url = link.getAttribute('href');
    copy(url).then(function () {
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