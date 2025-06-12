<template>
  <footer class="footer">
    <div class="container">
      <p class="footer__copyright">
      </p>
      <div class="built-tech">
        <span style="display: inline-flex; align-items: center;">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" viewBox="0 0 24 24" style="vertical-align: middle; margin-right: 0.5em;">
            <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 2v.01L12 13 4 6.01V6h16zm0 12H4V8.99l8 6.99 8-6.99V18z"/>
          </svg>
          Contact me: b19670630@gmail.com
        </span>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: "AppFooter"
};
</script>

<style scoped>
.footer {
  padding-block: 1rem;
  border-top: 1px solid hsl(214deg 9% 25% / 20%);
  margin-block-start: 40px;
}

.footer .container {
  flex-wrap: wrap;
  gap: 1rem;
  align-items: center;
  justify-content: space-between;
}

.footer__copyright {
  & em {
    text-emphasis: unset;
    font-style: normal;
    font-weight: var(--fw-bold);
    margin-inline-end: 0.25rem;
  }

  & span {
    font-weight: var(--fw-bold);
    opacity: 0.6;
    color: var(--text-color-default);
  }
}

.built-tech {
  & svg {
    display: inline-block;
    width: 40px;
  }

  a {
    vertical-align: middle;
  }

  a+a {
    margin-inline-start: 1rem;
  }
}

@media (--vw-lg) {
  .footer {
    font-size: var(--text-base);
  }
}

@media (--vw-sm) {
  .container {
    text-align: center;
  }

  .footer__copyright {
    order: 2;
  }

  .built-tech {
    order: 1;
    flex-basis: 100%;
  }
}
</style>
