<template>
    <div :style="{width}">
        <div v-if="title" class="form-title">
            {{title}}
        </div>
        <div class="form-body">
            <div class="item" :key="index" v-for="(element,index) in Object.keys(model)">
                <div class="cell-title">{{element}}</div>
                <div class="cell-value">
                    <!-- @change is equals to @blur / @input trigger as value changing -->
                    <input class="form-control" type="text" v-model="model[element]" @input="validate(element)">
                    <p v-if="errors[element]">{{errors[element]}}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import AsyncValidator from 'async-validator';

    const rules = {
        name: {
            type: "string",
            required: true,
        },
        email: {
            type: "email",
            required: true,
        }
    };

    export default {
        name: "GridForm",
        props: {
            width: {
                type: String,
                default: '90%'
            },
            title: {
                type: String,
                default: '表格 - 修改密碼'
            }
        },
        methods: {
            validate(field) { // validate is on form-item

                console.log(field + ' change');

                const validator = new AsyncValidator({[field]: rules[field]});

                // you need validate all fields that registered
                validator.validate(
                    {[field]: this.model[field]},
                    {firstFields: true}, // when field generates an error, no more validation
                    (errors) => {
                        // this.validateState = !errors ? 'success' : 'error';
                        // this.validateMessage = errors ? errors[0].message : '';

                        // something after validate
                        // callback(this.validateMessage, invalidFields);

                        if (errors) {
                            // validation failed, errors is an array of all errors
                            // fields is an object keyed by field name with an array of
                            // errors per field

                            const errMsg = errors.reduce((pre, curr) => pre + curr.message, '');
                            console.log('errMsg=', errMsg);
                            this.errors[field] = errMsg;
                            console.log('this.errors=', this.errors);

                        } else {
                            this.errors[field] = undefined;
                        }
                        // validation passed
                    });
            },
        },
        updated() {

            console.log('updated !!');
        },
        data() {

            return {
                errors: {},
                model: {
                    name: '談得賽',
                    company: 'WHO',
                    from: '非洲',
                    email: 'ttt@kkbox.com'
                }
            }
        }
    }
</script>

<style scoped>

    .form-title {
        height: 50px;
        padding: 10px;
        display: flex;
        align-items: center;
        border: 1px solid rgba(128, 137, 155, 0.5);
        font-weight: 900;
        font-size: 24px;
        color: #f0f8ff;
        background-color: #120dad;
    }

    /* 教學 : https://www.w3schools.com/css/css_grid_container.asp */
    .form-body {
        display: grid;
        grid-template-columns: 25% 25% 25% 25%; /* 4 column one row */
    }

    .item {
        border: 1px solid rgba(128, 137, 155, 0.3);
        display: flex;
        align-items: center;
        box-sizing: border-box;
    }

    .cell-title {
        background-color: #00ffff;
        padding: 10px;
        height: 100%;
        min-width: 80px;
        text-align: right;
    }

    .cell-value {
        padding: 0 12px 0 7px;
        height: 100%;
    }

</style>
