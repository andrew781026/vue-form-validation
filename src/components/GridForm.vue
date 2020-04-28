<template>
    <div :style="{width}">
        <div v-if="title" class="form-title">
            {{title}}
        </div>
        <div class="form-body">
            <div class="item" :key="n" v-for="n in 10">
                <div class="cell-title">{{String.fromCharCode(64+n)}}</div>
                <div class="cell-value">
                    <input class="input" type="text" v-model="value[n]">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Schema from 'async-validator';

    export default {
        name: "GridForm",
        props: {
            width: {
                type: String,
                default: '70%'
            },
            title: {
                type: String,
                default: '表格 - 修改密碼'
            }
        },
        data() {

            const descriptor = {
                name: {
                    type: "string",
                    required: true,
                    validator: (rule, value) => value === 'muji',
                },
                age: {
                    type: "number",
                    asyncValidator: (rule, value) => {
                        return new Promise((resolve, reject) => {
                            if (value < 18) {
                                reject("too young");  // reject with error message
                            } else {
                                resolve();
                            }
                        });
                    }
                }
            };

            const handleErrors = (errors, fields) => {

                console.error(errors);
                console.error(fields);
            };

            const validator = new Schema(descriptor);

            // watch the value change and validate again
            validator.validate({name: "muji"}, (errors, fields) => {
                if (errors) {
                    // validation failed, errors is an array of all errors
                    // fields is an object keyed by field name with an array of
                    // errors per field
                    return handleErrors(errors, fields);
                }
                // validation passed
            });

            // PROMISE USAGE
            validator.validate({name: "muji", age: 16})
                .then(() => {
                    // validation passed or without error message
                })
                .catch(({errors, fields}) => {
                    return handleErrors(errors, fields);
                });

            return {
                value: [
                    '',
                    '',
                    '',
                    '',
                    '',
                    '',
                    '',
                    '',
                    '',
                    '',
                ]
            }
        }
    }
</script>

<style scoped>

    .form-title {
        height: 30px;
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
        width: 60px;
        text-align: right;
    }

    .cell-value {
        padding: 0 12px 0 7px;
        height: 100%;
    }

    .input {
        width: 100%;
    }
</style>
