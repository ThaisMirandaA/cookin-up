<template>
    <footer class="footer-container">
        <h2 class="footer-text">Desenvolvido por Thaís | 2023 - Projeto fictício sem fins comerciais.</h2>
    </footer>
</template>

<style scoped>
.footer-container {
    background: var(--Verde-escuro, #263A29);
    display: flex;
    width: 1440px;
    padding: 24px 120px;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 10px;
}

.footer-text {
    color: var(--Creme, #FFFAF3);
    text-align: center;
    font-family: Nunito Sans;
    font-size: 18px;
    font-style: normal;
    font-weight: 400;
    line-height: 150%;
}

@media only screen and (max-width: 1300px) {
    .footer-container {
        padding: 1.5rem 3.75rem;
    }
}

@media only screen and (max-width: 767px) {
    .footer-container {
        padding: 1.5rem;
    }
}
</style>