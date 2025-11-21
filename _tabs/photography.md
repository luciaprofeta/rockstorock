---
title: Photography
icon: fas fa-camera
order: 4
permalink: /photography/
---

Commissions and shots in the wild. Click any image to view it larger.

<style>
  .photo-gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    grid-gap: 1rem;
    margin-top: 1.5rem;
  }

  .photo-gallery figure {
    margin: 0;
    cursor: pointer;
  }

  .photo-gallery img {
    width: 100%;
    height: auto;
    border-radius: 8px;
    display: block;
  }

  /* Lightbox */
  .lightbox-overlay {
    display: none;
    position: fixed;
    z-index: 9999;
    inset: 0;
    background: rgba(0, 0, 0, 0.85);
    align-items: center;
    justify-content: center;
  }

  .lightbox-overlay.is-visible {
    display: flex;
  }

  .lightbox-content {
    max-width: 90vw;
    max-height: 90vh;
    position: relative;
    text-align: center;
  }

  .lightbox-content img {
    width: 100%;
    height: auto;
    border-radius: 8px;
  }

  .copyright {
    margin-top: 0.8rem;
    color: #f5f5f5;
    font-size: 0.9rem;
    opacity: 0.85;
  }

  .lightbox-close {
    position: absolute;
    top: -12px;
    right: -12px;
    background: #ffffff;
    border-radius: 999px;
    border: none;
    width: 28px;
    height: 28px;
    font-size: 18px;
    line-height: 1;
    cursor: pointer;
  }
</style>

<div class="photo-gallery">

{% for photo in site.static_files %}
  {% if photo.path contains 'assets/img/photography/' %}
    <figure data-full="{{ photo.path }}">
      <img src="{{ photo.path }}" alt="Photography image" loading="lazy">
    </figure>
  {% endif %}
{% endfor %}

</div>



<div class="lightbox-overlay"
     id="lightbox"
     role="dialog"
     aria-modal="true"
     aria-label="Image preview">

  <div class="lightbox-content">
    <button class="lightbox-close" type="button" aria-label="Close">&times;</button>
    <img id="lightbox-image" src="" alt="">
    <div class="copyright">© Rocks2Rock</div>
  </div>

</div>

<script>
  (function() {
    const gallery = document.querySelector('.photo-gallery');
    const lightbox = document.getElementById('lightbox');
    const lightboxImage = document.getElementById('lightbox-image');
    const closeButton = lightbox.querySelector('.lightbox-close');

    if (!gallery || !lightbox) return;

    function openLightbox(src, alt) {
      lightboxImage.src = src;
      lightboxImage.alt = alt || '';
      lightbox.classList.add('is-visible');
      closeButton.focus();
    }

    function closeLightbox() {
      lightbox.classList.remove('is-visible');
      lightboxImage.src = '';
      lightboxImage.alt = '';
    }

    gallery.addEventListener('click', function(event) {
      const figure = event.target.closest('figure');
      if (!figure) return;

      const fullSrc = figure.getAttribute('data-full');
      const img = figure.querySelector('img');
      const alt = img ? img.alt : '';

      if (fullSrc) {
        openLightbox(fullSrc, alt);
      }
    });

    closeButton.addEventListener('click', closeLightbox);

    lightbox.addEventListener('click', function(event) {
      if (event.target === lightbox) {
        closeLightbox();
      }
    });

    document.addEventListener('keydown', function(event) {
      if (event.key === 'Escape' && lightbox.classList.contains('is-visible')) {
        closeLightbox();
      }
    });
  })();
</script>
