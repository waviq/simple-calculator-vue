<template>
    <div class="hello">
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">

        <div class="container">
            <div class="col-md-4">
                <h3>Simple Calculator</h3>
                <table class="table table-bordered">
                    <tbody>
                    <tr v-for="calculator in calculators">
                        <td>
                            <input type="number" v-model="calculator.number" class="form-control"
                                   :disabled="disabledStatus(calculator.status)">
                        </td>
                        <td>
                            <input v-model="calculator.status" type="checkbox" @click="checkList(calculator.status)"/>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            <button :disabled="disabledButtonOperator" type="button" class="btn btn-primary" @click="tambah()">+</button>
                            <button :disabled="disabledButtonOperator" type="button" class="btn btn-success" @click="kurang()">-</button>
                            <button :disabled="disabledButtonOperator" type="button" class="btn btn-info" @click="kali">x</button>
                            <button :disabled="disabledButtonOperator" type="button" class="btn btn-danger" @click="bagi">/</button>
                        </td>
                    </tr>
                    <tr>
                        <td colspan="2">
                            <hr/>
                        </td>
                    </tr>
                    <tr style="text-align: left">
                        <td>Hasil</td>
                        <td>{{resultTotal}}</td>
                    </tr>
                    </tbody>
                </table>
            </div>
        </div>

    </div>
</template>

<script>
    export default {
        name: 'HelloWorld',
        data() {
            return {
                number_1: '',
                number_2: '',
                number_3: '',
                calculators: [
                    {
                        number: 0,
                        status: true
                    },
                    {
                        number: 0,
                        status: true
                    },
                    {
                        number: 0,
                        status: false
                    }
                ],
                status: [],
                resultTotal: '',
                countCheck: parseInt(2)

            }
        },
        computed: {
            disabledButtonOperator()  {
                return this.countCheck <= 1;
            }
        },
        methods: {
            tambah() {
                let result = this.calculators.reduce((sum, data) => {
                    return sum + Number(data.number)
                }, 0)

                this.resultTotal = result
            },
            kurang() {
                let number_1 = Number(this.calculators[0].number)
                let number_2 = Number(this.calculators[1].number)
                let number_3 = Number(this.calculators[2].number)

                this.resultTotal = number_1 - number_2 - number_3
            },
            kali() {
                let numbers = []
                this.calculators.forEach((value) => {
                    if (value.status){
                        numbers.push(Number(value.number))
                    }
                })
                let result = numbers.reduce((a,b)=> a * b, 1)
                this.resultTotal = result


            },
            bagi() {
                let numbers = []
                let total = []
                this.calculators.forEach((value) => {
                    if (value.status){
                        numbers.push(Number(value.number))
                    }
                })

                let result = numbers.reduce((total, number)=> {
                    return total / number
                })

                this.resultTotal = result

            },
            disabledStatus(status) {
                return status !== true;
            },

            checkList(status) {
                if (status) {
                    this.countCheck = this.countCheck - status
                } else {
                    this.countCheck += 1
                }
               
                if (this.countCheck <=1) {
                    alert('minimum input is 2')
                }
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

    .table-bordered td, .table-bordered th {
        border: none;
    }

    .btn {
        margin-right: 10px;
    }

    hr {
        margin-top: 1rem;
        margin-bottom: 1rem;
        border: 0;
        border-top: 1px solid rgba(0, 0, 0, 0.1);
    }
</style>
