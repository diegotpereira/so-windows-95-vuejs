<template>
    <div class="pintar">
        <div class="arquivo-bar">
            <div class="link">
                Arquivo
                <div class="submenu">
                    <div class="link">Salvar</div>
                    <div class="link">Sair</div>
                </div>
            </div>
        </div>
        <div class="pintar-involucro">
            <div class="barraferramentas">
                <div 
                    v-for:="(cursor, index) in 6" 
                    v-bind:key="index"
                    v-on:click="this.definirCursor($event, index)"
                    :class="{ active: index + 1 === selecionarCursor }"
                    class="seletor-cursor">
                    <div    
                        class="cursor">
                        <span
                            v-bind:key="index"
                            v-bind:style="{
                            height: index + 5 + 'px',
                            width: index + 5 + 'px',
                            minHeight: index + 5 + 'px',
                            minWidth: index + 5 + 'px'
                            }">
                        </span>
                    </div>
                </div>
                <div class="seletor-cursor">
                    <div class="cursor">
                        <img 
                            width="9"
                            height="9"
                            :src="require('@/assets/icon/close.png')" 
                        />
                    </div>
                </div>
            </div>
            <div class="canvas-involucro">
                <canvas
                    width="634"
                    height="359"
                    ref="canvas"
                    @mousemove="moverMouse"
                    @mousedown="abaixarMouse"
                    >
                </canvas>
            </div>
        </div>
        <div class="cores">
            <div class="seletor-cor">
                <div 
                    class="cor"
                    v-bind:style="{
                        backgroundColor: '#' + this.selecionarCorEsquerda
                    }">
                </div>
                <div 
                    class="cor"
                    v-bind:style="{
                        backgroundColor: '#' + this.selecionarCorDireita
                    }">
                </div>
            </div>
            <div class="cor-selecionador">
                <div 
                    class="cor"
                    v-for="(cor, index) in cores" 
                    :key="index"
                    v-on:click.left.stop="definirCorEsquerda($event, cor)"
                    v-on:click.right.stop="definirCorDireita($event, cor)"
                    v-bind:style="{
                        backgroundColor: '#' + cor,
                    }">
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'paginaPintar',
    data() {
        return {
            ehMouseClicado: false,
            ehMouseNoCanvas: false,
            ultimoX: 0,
            ultimoY: 0,
            atualX: 0,
            atualY: 0,
            canvas: "",
            selecionarCursor: 1,
            selecionarCorEsquerda: "000000",
            selecionarCorDireita: "FFFFFF",
            cores: [
                "000000",
                "808080",
                "800000",
                "808000",
                "008000",
                "008080",
                "000080",
                "800080",
                "808040",
                "004040",
                "0080ff",
                "004080",
                "8000ff",
                "804000",
                "FFFFFF",
                "c0c0c0",
                "ff0000",
                "ffff00",
                "00ff00",
                "00ffff",
                "0000ff",
                "ff00ff",
                "ffff80",
                "00ff80",
                "80ffff",
                "8080ff",
                "ff0080",
                "ff8040",
            ],
        }
    },
    mounted: function() {
        this.canvas = this.$refs.canvas.getContext("2d");
    },
    methods: {
        definirCursor(e, indice) {
            this.selecionarCursor = indice + 1;
        },
        definirCorEsquerda(e, cor) {
            this.selecionarCorEsquerda = cor;
        },
        definirCorDireita(e, cor) {
            e.preventDefault();
            e.stopPropagation();
            this.selecionarCorDireita = cor;
        },
        abaixoMouse(e) {
            const { x, y } = this.$refs.canvas.getBoundingClientRect();

            this.ultimoX = e.clientX - x;
            this.ultimoY = e.clientY - y;
        },
        moverMouse(e) {
            e.preventDefault();
            e.stopPropagation();

            if(e.buttons !== 1 && e.buttons !== 2)
            return;

            this.desenhar(e);
        },
        desenhar(e) {
            const { x, y } = this.$refs.canvas.getBoundingClientRect();
            const novoX = e.clientX - x;
            const novoY = e.clientY - y;

            this.canvas.beginPath();
            this.canvas.lineWidth = this.selecionarCursor;
            this.canvas.moveTo(this.ultimoX, this.ultimoY);
            this.canvas.lineTo(novoX, novoY);

            if(e.buttons == 1) {
                this.canvas.strokeStyle = "#" + this.selecionarCorEsquerda;

            } else if (e.buttons == 2) {
                this.canvas.strokeStyle = "#" + this.selecionarCorDireita;

            } else {
                this.canvas.strokeStyle = "#" + this.selecionarCorEsquerda;
            }
            this.canvas.stroke();
            this.canvas.closePath();

            this.ultimoX = novoX;
            this.ultimoY = novoY;
        }
    }
}
</script>
<style lang="scss" scoped>
.pintar {
    overflow: hidden;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: stretch;
    .arquivo-bar {
        background-color: rgba(191, 193 , 192, 1);
        padding: 2px 0px 0px 0px;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: flex-start;
        user-select: none;
        .link {
            cursor: default;
            padding: 0px 4px 0px 4px;
            display: flex;
            align-items: center;
            justify-content: flex-start;
            height: 18px;
            position: relative;
            &:after {
                content: "";
                position: absolute;
                bottom: 4px;
                left: 4px;
                width: 6px;
                height: 1px;
                background: #000000;
            }
            &:hover,
            &:active {
                background-color: $highlightV95;
                color: white;
                &:after {
                    content: "";
                    position: absolute;
                    bottom: 4px;
                    left: 4px;
                    width: 6px;
                    height: 1px;
                    background: #FFFFFF;
                }
                > .submenu {
                    display: block;
                }
            }
            .submenu {
                @include v95;
                color: initial;
                position: absolute;
                min-width: 122px;
                top: 100%;
                left: 0;
                display: none;
                padding: 2px;
                z-index: 10;
                user-select: none;
                background-color: rgba(191, 193, 192, 1);
            }
        }
    }
    .pintar-involucro {
        height: 100%;
        width: 100%;
        display: flex;
        flex-direction: row;
        align-items: stretch;
        justify-content: space-evenly;
        overflow: hidden;
        .canvas-involucro {
            @include v95Hover;
            height: 100%;
            width: 100%;
            overflow: auto;
        }
    }
    .barraferramentas {
        @include v95Hover;
        overflow: hidden;
        width: 48px;
        padding: 2px 2px 0px 2px;
        .seletor-cursor {
            @include v95;
            height: 24px;
            width: 24px;
            margin-top: 1px;
            margin-bottom: 5px;
            .cursor {
                height: 100%;
                width: 100%;
                display: flex;
                align-items: center;
                justify-content: center;
                span {
                    display: block;
                    border-radius: 100px;
                    background-color: black;
                }
            }
            &:active,
            &:active {
                @include v95Hover;
            }
        }
    }
    .cores {
        padding-top: 2px;
        display: flex;
        flex-direction: row;
        align-items: flex-start;
        justify-content: flex-start;
    }
    .seletor-cor {
        @include v95Hover;
        min-width: 43px;
        min-height: 43px;
        width: 44px;
        height: 43px;
        position: relative;
        .cor {
            margin: 1px 0px 0px 1px;
            &:nth-of-type(1) {
                z-index: 2 !important;
                position: absolute;
                left: 7px;
                top: 7px;
            }
            &:nth-of-type(2) {
                z-index: 1 !important;
                position: absolute;
                left: 17px;
                top: 17px;
            }
        }
    }
    .cor-selecionador {
        @include v95Hover;
        max-width: 258px;
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        padding-bottom: 3px;
        padding-left: 3px;
    }
    .cor {
        @include v95Hover;
        width: 16px;
        height: 16px;
        background: red;
        margin-right: 2px;
        margin-top: 3px;
        box-shadow: #000000 1px 1px 0px 0px inset;
    }
    canvas {
        width: 632px;
        height: 357px;
        object-fit: contain;
        background-color: white;
    }
}
</style>