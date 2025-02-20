<template>
    <div class="menu">
        <div class="menu-container">
            <h1>Escolha seus sabores</h1>

            <ul class="pizza-list">
                <li v-for="(sabor, index) in sabores" :key="index">
                    <label>
                        <input type="checkbox" :value="sabor" v-model="selecionados" />
                        {{ sabor }}
                    </label>
                </li>
            </ul>

            <button @click="enviarSabores" :disabled="selecionados.length === 0">
                Enviar Pedido
            </button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            sabores: [
                "Calabresa",
                "Mussarela",
                "Frango com Catupiry",
                "Portuguesa",
                "Quatro Queijos",
                "Pepperoni",
                "Margherita",
                "Chocolate",
                "Romeu e Julieta"
            ],
            selecionados: [] // Lista de sabores marcados
        };
    },
    methods: {
        async enviarSabores() {
            try {
                const response = await fetch("https://api.exemplo.com/pedidos", {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json"
                    },
                    body: JSON.stringify({ sabores: this.selecionados })
                });

                if (response.ok) {
                    alert("Pedido enviado com sucesso!");
                    this.selecionados = [];
                } else {
                    alert("Erro ao enviar pedido.");
                }
            } catch (error) {
                console.error("Erro na requisição:", error);
                alert("Erro ao conectar com o servidor.");
            }
        }
    }
};
</script>

<style scoped>
.menu {
    display: flex;
    /* justify-content: center; */
    /* align-items: center; */
    padding: 20px;
    height: 100vh;
    background-color: #e5c099;
}

.pizza-list {
    list-style: none;
    padding: 0;
}

.pizza-list li {
    margin: 5px 0;
}

label {
    display: flex;
    align-items: center;
    cursor: pointer;
    font-size: 18px;
}

input[type="checkbox"] {
    margin-right: 10px;
    transform: scale(1.2);
    cursor: pointer;
}

button {
    margin-top: 15px;
    padding: 10px 20px;
    border: none;
    background: #264653;
    color: white;
    cursor: pointer;
    border-radius: 5px;
    transition: 0.3s;
}

button:disabled {
    background: gray;
    cursor: not-allowed;
}

button:hover:not(:disabled) {
    background: #1d3557;
}
</style>