<script lang="ts">
import type IReceita from '@/interfaces/IReceita';
import { obterReceitas } from '@/http';
import BotaoPrincipal from './BotaoPrincipal.vue';
import CardReceitas from './CardReceitas.vue';
import type { PropType } from 'vue';
import { itensDeLista1EstaoEmLista2 } from '@/operacoes/listas';

export default {
    props: {
        ingredientes: { type: Array as PropType<string[]>, required: true }
    },
    data() {
        return {
            receitas: [] as IReceita[],
        };
    },
    async created() {
        const receitasApi = await obterReceitas();
        
        this.receitas = receitasApi.filter((receita) => {
            const receitaAtende = itensDeLista1EstaoEmLista2(receita.ingredientes.map(ingrediente => ingrediente.toLowerCase()),
                this.ingredientes.map(ingrediente => ingrediente.toLowerCase()));

            return receitaAtende;
        })
    },
    components: { BotaoPrincipal, CardReceitas },
    emits: ['buscarIngredientes']
}
</script>

<template>
    <section class="mostrar-receitas">
        <h1 class="cabecalho titulo-receitas">Receitas</h1>
        <h2 class="subtitulo-receitas">Resultados encontrados: {{ receitas.length }}</h2>
        <p class="paragrafo-lg paragrafo-receitas" v-if="receitas.length">
            Veja as opções de receitas que encontramos com os ingredientes que você tem por aí!
        </p>
        <div v-else class="container-receita-nao-encontrada">
            <p class="paragrafo-lg paragrafo-receitas">
                Ops, não encontramos resultados para sua combinação. Vamos tentar de novo?
            </p>
            <img class="imagem-receita-nao-encontrada" :src="'src/assets/images/sem-receitas.png'"
                :alt="'Desenho de um ovo quebrado. A gema tem um rosto com uma expressão triste.'">
        </div>

        <ul class="categorias">
            <li v-for="receita in receitas" :key="receita.nome">
                <CardReceitas :receitas="receita" />
            </li>
        </ul>
        <BotaoPrincipal :texto="'Editar lista'" @click="$emit('buscarIngredientes')" />
    </section>
</template>

<style scoped>
.mostrar-receitas {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.titulo-receitas {
    color: var(--verde-medio, #3D6D4A);
    display: block;
    margin-bottom: 1.5rem;
}

.subtitulo-receitas {
    color: var(--Verde-mdio, #3D6D4A);
    text-align: center;
    font-family: Nunito Sans;
    font-size: 22px;
    font-style: normal;
    font-weight: 400;
    line-height: 150%;
}

.paragrafo-receitas {
    margin-bottom: 2rem;
    margin-top: 2rem;
}

.categorias {
    margin-bottom: 1rem;
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    flex-wrap: wrap;
}

.container-receita-nao-encontrada {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    align-self: stretch;
}

.imagem-receita-nao-encontrada {
    width: 300px;
    height: 300px;
}
</style>