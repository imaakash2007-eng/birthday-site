/* =========================================================
   HAPPY BIRTHDAY SITE — SCRIPT
   Sections: typewriter, surprise reveal, ambient hearts/sparkles,
   scroll reveal, confetti, gift box, music player.
   ========================================================= */

document.addEventListener('DOMContentLoaded', () => {

  /* ---------------------------------------------------------
     0. TYPEWRITER — landing subtitle
     --------------------------------------------------------- */
  const typewriterTarget = document.getElementById('typewriterTarget');
  const typewriterText = "Today is your special day!"; // EDIT this line if you'd like
  let twIndex = 0;

  function typeNext() {
    if (twIndex <= typewriterText.length) {
      typewriterTarget.textContent = typewriterText.slice(0, twIndex);
      twIndex++;
      setTimeout(typeNext, 45);
    } else {
      typewriterTarget.classList.add('done');
    }
  }
  setTimeout(typeNext, 500);

  /* ---------------------------------------------------------
     1. AMBIENT FLOATING HEARTS + SPARKLES (background layer)
     --------------------------------------------------------- */
  const ambientLayer = document.getElementById('ambientLayer');
  const heartEmojis = ['💗', '💕', '🌸'];
  const sparkleEmojis = ['✨', '⋆', '✧'];

  function spawnFloaty() {
    const el = document.createElement('span');
    const isSparkle = Math.random() > 0.6;
    el.className = 'floaty' + (isSparkle ? ' sparkle' : '');
    el.textContent = isSparkle
      ? sparkleEmojis[Math.floor(Math.random() * sparkleEmojis.length)]
      : heartEmojis[Math.floor(Math.random() * heartEmojis.length)];

    const left = Math.random() * 100;
    const duration = 9 + Math.random() * 8;
    const size = isSparkle ? (0.7 + Math.random() * 0.8) : (1 + Math.random() * 1.1);
    const drift = (Math.random() * 120 - 60) + 'px';

    el.style.left = left + 'vw';
    el.style.fontSize = size + 'rem';
    el.style.animationDuration = duration + 's';
    el.style.setProperty('--drift', drift);

    ambientLayer.appendChild(el);
    setTimeout(() => el.remove(), duration * 1000 + 500);
  }

  // Gentle, ongoing ambience across the whole site
  setInterval(spawnFloaty, 900);
  for (let i = 0; i < 5; i++) setTimeout(spawnFloaty, i * 300);

  /* ---------------------------------------------------------
     2. LANDING → OPEN SURPRISE
     --------------------------------------------------------- */
  const landing = document.getElementById('landing');
  const mainSite = document.getElementById('mainSite');
  const openBtn = document.getElementById('openSurpriseBtn');

  document.body.classList.add('locked');

  openBtn.addEventListener('click', () => {
    landing.classList.add('is-leaving');
    burstConfettiAt(document.getElementById('confettiCanvas'), 90);

    setTimeout(() => {
      landing.style.display = 'none';
      document.body.classList.remove('locked');
      mainSite.classList.add('is-visible');
      mainSite.scrollIntoView({ behavior: 'instant' in window ? 'auto' : 'auto' });
      initScrollReveal();
    }, 850);
  });

  /* ---------------------------------------------------------
     3. SCROLL REVEAL (fade-in-up elements)
     --------------------------------------------------------- */
  function initScrollReveal() {
    const revealEls = document.querySelectorAll('.fade-in-up');
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('in-view');
          observer.unobserve(entry.target);
        }
      });
    }, { threshold: 0.2 });

    revealEls.forEach((el) => observer.observe(el));
  }

  /* ---------------------------------------------------------
     4. CONFETTI (canvas-based, lightweight)
     --------------------------------------------------------- */
  const confettiColors = ['#F7C9D9', '#EF9DBC', '#C6ADEA', '#D9B36C', '#FFFFFF'];

  function burstConfettiAt(canvas, count = 70) {
    if (!canvas) return;
    const ctx = canvas.getContext('2d');
    const parent = canvas.parentElement;
    const resize = () => {
      canvas.width = parent.clientWidth;
      canvas.height = parent.clientHeight;
    };
    resize();

    const pieces = Array.from({ length: count }, () => ({
      x: canvas.width / 2 + (Math.random() * 200 - 100),
      y: canvas.height * 0.3,
      vx: (Math.random() - 0.5) * 9,
      vy: Math.random() * -9 - 3,
      size: 5 + Math.random() * 6,
      color: confettiColors[Math.floor(Math.random() * confettiColors.length)],
      rotation: Math.random() * 360,
      rotSpeed: (Math.random() - 0.5) * 12,
      life: 0,
    }));

    let frame = 0;
    const maxFrames = 140;

    function tick() {
      frame++;
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      pieces.forEach((p) => {
        p.vy += 0.22; // gravity
        p.x += p.vx;
        p.y += p.vy;
        p.rotation += p.rotSpeed;

        ctx.save();
        ctx.translate(p.x, p.y);
        ctx.rotate((p.rotation * Math.PI) / 180);
        ctx.fillStyle = p.color;
        ctx.fillRect(-p.size / 2, -p.size / 2, p.size, p.size * 0.6);
        ctx.restore();
      });

      if (frame < maxFrames) {
        requestAnimationFrame(tick);
      } else {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
      }
    }
    tick();
  }

  // Trigger confetti once the birthday-message section scrolls into view
  const birthdaySection = document.getElementById('birthday');
  const birthdayCanvas = document.getElementById('confettiCanvas');
  let birthdayFired = false;

  const birthdayObserver = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting && !birthdayFired) {
        birthdayFired = true;
        burstConfettiAt(birthdayCanvas, 110);
      }
    });
  }, { threshold: 0.4 });
  birthdayObserver.observe(birthdaySection);

  /* ---------------------------------------------------------
     5. GIFT BOX SURPRISE
     --------------------------------------------------------- */
  const giftBox = document.getElementById('giftBox');
  const giftReveal = document.getElementById('giftReveal');
  const giftCanvas = document.getElementById('giftConfettiCanvas');
  let giftOpened = false;

  giftBox.addEventListener('click', () => {
    if (giftOpened) return;
    giftOpened = true;
    giftBox.classList.add('is-opened');
    setTimeout(() => giftReveal.classList.add('is-visible'), 300);
    burstConfettiAt(giftCanvas, 100);
  });

  /* ---------------------------------------------------------
     6. MUSIC PLAYER (no autoplay — user must press play)
     --------------------------------------------------------- */
  const bgAudio = document.getElementById('bgAudio');
  const musicToggle = document.getElementById('musicToggle');
  const musicIcon = document.getElementById('musicIcon');
  let isPlaying = false;

  musicToggle.addEventListener('click', () => {
    if (!isPlaying) {
      bgAudio.play().catch(() => {
        // Placeholder audio file may not exist yet — replace music/birthday-song.mp3
        console.info('Add your own audio file at music/birthday-song.mp3 to enable playback.');
      });
      musicIcon.textContent = '⏸️';
      musicToggle.classList.add('is-playing');
      musicToggle.setAttribute('aria-label', 'Pause music');
      isPlaying = true;
    } else {
      bgAudio.pause();
      musicIcon.textContent = '🎵';
      musicToggle.classList.remove('is-playing');
      musicToggle.setAttribute('aria-label', 'Play music');
      isPlaying = false;
    }
  });

  // Re-size active confetti canvases on window resize
  window.addEventListener('resize', () => {
    [birthdayCanvas, giftCanvas].forEach((canvas) => {
      if (canvas && canvas.parentElement) {
        canvas.width = canvas.parentElement.clientWidth;
        canvas.height = canvas.parentElement.clientHeight;
      }
    });
  });
});