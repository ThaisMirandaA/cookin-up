<script lang="ts">
import type IReceita from '@/interfaces/IReceita';
import type { PropType } from 'vue';

export default {
    props: {
        receitas: { type: Object as PropType<IReceita>, required: true }
    }
}
</script>

<template>
    <article class="receita">
        <header class="receita__cabecalho">
            <img :src="`/imagens/receitas/${receitas.imagem}`" alt="" class="receita__imagem">
        </header>
        <div class="nome__container">
            <h2 class="paragrafo-lg receita__nome">{{ receitas.nome }}</h2>

        </div>
        <ul class="receita__ingredientes">
            <li v-for="receita in receitas.ingredientes" :key="receita"></li>
        </ul>
    </article>
</template>

<style scoped>
.receita {
    display: flex;
    width: 312px;
    height: 246px;
    max-width: 312px;
    flex-direction: column;
    align-items: center;
    border-radius: 16px;
    background: var(--Branco, #FFF);
    box-shadow: 4px 4px 12px 0px rgba(68, 68, 68, 0.08);
}

.receita__cabecalho {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
}

.receita__imagem {
    width: 312px;
    height: 150px;
    flex-shrink: 0;
    align-self: stretch;
    border-radius: 16px 16px 0px 0px;
    background: url(<path-to-image>), lightgray 50% / cover no-repeat;
}

.nome__container {
    display: flex;
    padding: 32px 0px;
    align-items: center;
    gap: 10px;
    background: var(--Branco, #FFF);
}

.receita__nome {
    color: var(--Cinza, #444);
    text-align: center;
    font-family: Nunito Sans;
    font-size: 18px;
    font-style: normal;
    font-weight: 700;
    line-height: 150%;
}

.receita__ingredientes {
    display: flex;
    justify-content: center;
    gap: 0.5rem;
    flex-wrap: wrap;
}
</style>