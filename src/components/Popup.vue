<template>
    <div class="popup" id="popup" v-bind:class="{open: main.isActive}">
        <div class="popup__body">
            <div class="popup__content">
                <div class="popup__title-container">
                <h3 class="popup__title">Налоговый вычет</h3>
                <img src="../../public/img/Cross.svg" class="popup__close" v-on:click="main.isActive=false">
                </div>
                <p class="popup__paragraph">
                    Используйте налоговый вычет чтобы погасить <br class="popup__br3" />ипотеку <br class="popup__br2" />досрочно. <br class="popup__br1" />
                    Размер налогового вычета <br class="popup__br3" />составляет <br class="popup__br2" />не более 13% от своего <br class="popup__br1" />
                    официального <br class="popup__br3" />годового дохода.
                </p>
                <form class="popup__form" @submit.prevent>
                    <p class="popup__form-pargraph">Ваша зарплата в месяц</p>
                    <input type="text" placeholder="Введите данные" class="popup__form-inut" 
                        v-model="inputValue"
                        >
                    <div class="popup__calculate-btn" v-on:click="CalculateTax">
                        Рассчитать</div>
                    <div class="checkboxWrapper" v-bind:class="{open: main.isOpenCheckbox}">
                        <p class="popup__calculate-paragraph">Итого можете внести <br class="popup__br3" />в качестве досрочных:</p>
                        <ul>
                            <li v-for="valueCheckbox in sumCheckArr">
                                <div class="form__checkbox-container">
                                    <div class="form-checkbox">
                                        <input :id="valueCheckbox" type="checkbox" name="money" class="checkbox-input" :checked="sumCheckArr.length==valueCheckbox? false : true">
                                        <label :for="valueCheckbox" class="checkbox-label">{{Math.ceil(taxArray[valueCheckbox-1]) +" рублей &nbsp"}} <span class="checkbox-span">в {{valueCheckbox}}-ый год</span></label>
                                    </div>
                                    <hr>
                                </div>
                            </li>
                        </ul>
                    </div>
                    <div class="form__question">
                        <span class="form__question-span">Что уменьшаем?</span>
                        <div class="form__question-btns">
                            <button class="form__question-payment">Платеж</button>
                            <button class="form__question-term">Срок</button>
                        </div>
                    </div>
                    <button class="form__submit">Добавить</button>
                </form>
            </div>
        </div>
    </div>
</template>
<script>

export default {
    data: () => ({
        specialId: Math.ceil(Math.random()*100),
        sumCheck: null,
        inputValue: "",
        valueCheckbox: 0,
        taxObject: {
            taxArray: null,
            sumCheckArr: null,
        },
    }),
    props: {
        main: {
            type: Object,
            required: true
        },
    },
    methods: {
        CalculateTax() {
            let sumCheck = Math.ceil(260000/(this.inputValue*12*0.13)) 
            this.main.isOpenCheckbox = false
            this.sumCheckArr = []
            this.taxArray = []
            for (let i = 1; i<=sumCheck; i++) {
                this.sumCheckArr.push(i)
            }
            for (let i=1; i<=this.sumCheckArr.length; i++) {
                if(i!=this.sumCheckArr.length) {
                    this.taxArray.push(this.inputValue*12*0.13)
                } else {
                    this.taxArray.push(260000 - (this.inputValue*12*0.13*(i-1)))
                }
            }
            console.log("Количесто выплат :",this.sumCheckArr)
            console.log("Cуммы выплат :",this.taxArray)
            return this.sumCheckArr
        }
    },
}
</script>
<style src='../../public/styles/popup.css'></style>

