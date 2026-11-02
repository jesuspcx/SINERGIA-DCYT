// Inicialización de Iconos Lucide y Funcionalidades
document.addEventListener("DOMContentLoaded", () => {
  // Renderizar iconos iniciales
  if (window.lucide) {
    window.lucide.createIcons();
  }

  // Lógica de Modo Oscuro / Claro
  const themeToggleBtn = document.getElementById("theme-toggle");

  function syncThemeIcons() {
    if (window.lucide) {
      window.lucide.createIcons();
    }
  }

  if (themeToggleBtn) {
    themeToggleBtn.addEventListener("click", () => {
      const isDark = document.documentElement.classList.toggle("dark");
      if (isDark) {
        localStorage.setItem("theme", "dark");
      } else {
        localStorage.setItem("theme", "light");
      }
      syncThemeIcons();
    });
  }

  // Toggle de Menú Móvil
  const mobileBtn = document.getElementById("mobile-menu-btn");
  const mobileMenu = document.getElementById("mobile-menu");
  const mobileLinks = document.querySelectorAll(".mobile-nav-link");

  if (mobileBtn && mobileMenu) {
    mobileBtn.addEventListener("click", () => {
      mobileMenu.classList.toggle("hidden");
    });

    mobileLinks.forEach(link => {
      link.addEventListener("click", () => {
        mobileMenu.classList.add("hidden");
      });
    });
  }

  // Resaltado de enlaces en Navbar al hacer scroll
  const sections = document.querySelectorAll("section[id]");
  const navLinks = document.querySelectorAll(".nav-link");

  window.addEventListener("scroll", () => {
    let current = "";
    const scrollY = window.pageYOffset;

    sections.forEach(section => {
      const sectionHeight = section.offsetHeight;
      const sectionTop = section.offsetTop - 120;
      const sectionId = section.getAttribute("id");

      if (scrollY > sectionTop && scrollY <= sectionTop + sectionHeight) {
        current = sectionId;
      }
    });

    navLinks.forEach(link => {
      link.classList.remove("text-ucla-700", "dark:text-sky-400", "bg-ucla-50", "dark:bg-slate-800");
      if (link.getAttribute("href") === `#${current}`) {
        link.classList.add("text-ucla-700", "dark:text-sky-400", "bg-ucla-50", "dark:bg-slate-800");
      }
    });
  });
});