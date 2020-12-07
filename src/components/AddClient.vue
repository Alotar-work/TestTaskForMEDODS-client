<template>
    <form class="container" @submit.prevent="submit">
        <div class="titleDiv">Общая информация:</div>
        <div class="lineDiv"></div>
        <div class="row">
            <div>
                <div class="labelOfField">Фамилия*</div>
                <input type="text" v-model="$v.secondName.$model" :class="{ 'error': $v.secondName.$error }" @input="status($event.target.value)"/>
                <div class="errorMessage" v-if="!$v.secondName.required && $v.secondName.$error">Обязательное поле</div>
                <div class="errorMessage" v-if="!$v.secondName.minLength">Минимальная длина поля {{$v.secondName.$params.minLength.min}}</div>
            </div>
            <div>
                <div class="labelOfField">Имя*</div>
                <input type="text" v-model="$v.firstName.$model" :class="{ 'error': $v.firstName.$error }" @input="status($event.target.value)"/>
                <div class="errorMessage" v-if="!$v.firstName.required && $v.firstName.$error">Обязательное поле</div>
                <div class="errorMessage" v-if="!$v.firstName.minLength">Минимальная длина поля {{$v.firstName.$params.minLength.min}}</div>
            </div>
            <div>
                <div class="labelOfField">Отчество</div>
                <input type="text" v-model="$v.middleName.$model" :class="{ 'error': $v.middleName.$error }" @input="status($event.target.value)"/>
                <div class="errorMessage" v-if="!$v.middleName.minLength">Минимальная длина поля {{$v.middleName.$params.minLength.min}}</div>
            </div>
        </div>
        <div class="row">
            <div>
                <div class="labelOfField">Дата рождения*</div>
                <input type="date" v-model="$v.dateOfBirth.$model" :class="{ 'error': $v.dateOfBirth.$error }" @input="status($event.target.value)">
                <div class="errorMessage" v-if="!$v.dateOfBirth.required && $v.dateOfBirth.$error">Обязательное поле</div>
                <div class="errorMessage" v-if="!$v.dateOfBirth.maxDate">Неверная дата</div>
            </div>
            <div>
                <div class="labelOfField">Пол</div>
                <select v-model="gender">
                    <option value="Мужчина">Мужчина</option>
                    <option value="Женщина">Женщина</option>
                </select>
            </div>
            <div>
                <div class="labelOfField">Номер телефона*</div>
                <input type="text" maxlength="11" v-model="$v.phone.$model" :class="{ 'error': $v.phone.$error }" @input="status($event.target.value)">
                <div class="errorMessage" v-if="!$v.phone.required && $v.phone.$error">Обязательное поле</div>
                <div class="errorMessage" v-if="!$v.phone.minLength">Минимальная длина поля {{$v.phone.$params.minLength.min}}</div>
                <div class="errorMessage" v-if="!$v.phone.numeric">Недопустимые символы</div>
                <div class="errorMessage" v-if="!$v.phone.firstSymbol && $v.phone.$error">Неверный формат (7xxxxxxxxxx)</div>
            </div>
        </div>
        <div class="row">
            <div>
                <div class="labelOfField">Группа клиентов*</div>
                <select size="3" multiple v-model="$v.clientGroup.$model">
                    <option value="VIP">VIP</option>
                    <option value="Проблемные">Проблемные</option>
                    <option value="ОМС">ОМС</option>
                </select>
                <div class="errorMessage" v-if="!$v.clientGroup.required && $v.clientGroup.$error">Обязательное поле</div>
            </div>
            <div>
                <div class="labelOfField">Лечащий врач</div>
                <select v-model="attendingDoctor">
                    <option value="Иванов">Иванов</option>
                    <option value="Захаров">Захаров</option>
                    <option value="Чернышева">Чернышева</option>
                </select>
            </div>
            <div>
                <div class="row">
                    <div class="labelOfField">Не отправлять СМС</div>
                    <div><input type="checkbox" v-model="isSendSMS"/></div>
                </div>
            </div>
        </div>

        <div class="titleDiv">Адрес:</div>
        <div class="lineDiv"></div>
        <div class="row">
            <div>
                <div class="labelOfField">Индекс</div>
                <input type="text" v-model="$v.index.$model" :class="{ 'error': $v.index.$error }" @input="status($event.target.value)"/>
                <div class="errorMessage" v-if="!$v.index.numeric">Недопустимые символы</div>
            </div>
            <div>
                <div class="labelOfField">Страна</div>
                <input type="text" v-model="country"/>
            </div>
            <div>
                <div class="labelOfField">Область</div>
                <input type="text" v-model="region"/>
            </div>
        </div>
        <div class="row">
            <div>
                <div class="labelOfField">Город*</div>
                <input type="text" v-model="$v.city.$model" :class="{ 'error': $v.city.$error }" @input="status($event.target.value)"/>
                <div class="errorMessage" v-if="!$v.city.required && $v.city.$error">Обязательное поле</div>
            </div>
            <div>
                <div class="labelOfField">Улица</div>
                <input type="text" v-model="street"/>
            </div>
            <div>
                <div class="labelOfField">Дом</div>
                <input type="text" v-model="houseNumber"/>
            </div>
        </div>

        <div class="titleDiv">Паспорт:</div>
        <div class="lineDiv"></div>
        <div class="row">
            <div>
                <div class="labelOfField">Тип документа*</div>
                <select v-model="$v.documentType.$model" :class="{ 'error': $v.documentType.$error }" @input="status($event.target.value)">
                    <option value="Паспорт">Паспорт</option>
                    <option value="Свидетельство о рождении">Свидетельство о рождении</option>
                    <option value="Вод. удостоверение">Вод. удостоверение</option>
                </select>
                <div class="errorMessage" v-if="!$v.documentType.required && $v.documentType.$error">Обязательное поле</div>
            </div>
            <div>
                <div class="labelOfField">Серия</div>
                <input type="text" v-model="series"/>
            </div>
            <div>
                <div class="labelOfField">Номер</div>
                <input type="text" v-model="number"/>
            </div>
        </div>
        <div class="row">
            <div>
                <div class="labelOfField">Кем выдан</div>
                <input type="text" v-model="issuenBy"/>
            </div>
            <div>
                <div class="labelOfField">Дата выдачи*</div>
                <input type="date" v-model="$v.dateOfIssue.$model" :class="{ 'error': $v.dateOfIssue.$error }" @input="status($event.target.value)">
                <div class="errorMessage" v-if="!$v.dateOfIssue.required && $v.dateOfIssue.$error">Обязательное поле</div>
                <div class="errorMessage" v-if="!$v.dateOfIssue.maxDate">Неверная дата</div>
            </div>
        </div>
        <div class="row">
            <button type="submit">Создать клиента</button>
        </div>
              
        <div class="note">*Поле обязательное для заполнения.</div>
    </form>
</template>

<script>
import { required, minLength, numeric } from 'vuelidate/lib/validators'

export default {
    name: 'AddClient',
    props: {
    },
    data() {
        return {
            secondName: '',
            firstName: '',
            middleName: '',
            dateOfBirth: null,
            gender: 'Мужчина',
            phone: '',
            clientGroup: [],
            attendingDoctor: 'Иванов',
            isSendSMS: false,
            index: '',
            country: '',
            region: '',
            city: '',
            street: '',
            houseNumber: '',
            documentType: '',
            series: '',
            number: '',
            issuenBy: '',
            dateOfIssue: null
        }
    },
    validations: {
        secondName: {
            required,
            minLength: minLength(2)
        },
        firstName: {
            required,
            minLength: minLength(2)
        },
        middleName: {
            minLength: minLength(2)
        },
        dateOfBirth: {
            required,
            maxDate(val) {
                return new Date() > new Date(val);
            }   
        },
        phone: {
            required,
            minLength: minLength(11),
            numeric,
            firstSymbol(val){
                return val[0] == "7"
            }
        },
        clientGroup: {
            required
        },
        index: {
            numeric
        },
        city: {
            required
        },
        documentType: {
            required
        },
        dateOfIssue:{
            required,
            maxDate(val) {
                return new Date() > new Date(val);
            }
        }
    },
    methods: {
        status(validation) {
            return {
                error: validation.$error
            }
        },
        submit() {
            this.$v.$touch()
            if (this.$v.$invalid) {
                alert("Проверьте правильность заполнения полей")
            } else {
                Object.assign(this.$data, getDefaultData());
                this.$nextTick(() => { this.$v.$reset() })
                alert("Клиент успешно создан!")
            }
        }
    }
}

function getDefaultData() {
    return {    
        secondName: '',
        firstName: '',
        middleName: '',
        dateOfBirth: null,
        gender: 'Мужчина',
        phone: '',
        clientGroup: [],
        attendingDoctor: 'Иванов',
        isSendSMS: false,
        index: '',
        country: '',
        region: '',
        city: '',
        street: '',
        houseNumber: '',
        documentType: '',
        series: '',
        number: '',
        issuenBy: '',
        dateOfIssue: null,
        submitStatus: null        
    }
}

</script>

<style>
</style>