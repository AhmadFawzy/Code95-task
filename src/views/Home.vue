<template>
  <div class="row justify-content-center mx-0">
    <div class="col-lg-8 col-md-11 p-0">
      <!-- Step One -->
      <div v-show="step == 1" class="step-one">
        <h1 class="my-5 text-center">نموذج طلب المنتج "هندسة الموسم"</h1>
        <h5 class="mb-5 text-center">بيانات المنظمة</h5>
        <div class="row mb-5">
          <div class="col-md-6 mb-2">
            <label for="organizeName" class="form-label">اسم المنظمة <span class="required">*</span></label>
            <input type="text" class="form-control" id="organizeName" v-model="organizeName" required>
          </div>
          <div class="col-md-6">
            <label for="organizeActivity" class="form-label">نشاط المنظمة <span class="required">*</span></label>
            <input type="text" class="form-control" id="organizeActivity" v-model="organizeActivity" required>
          </div>
        </div>

        <div class="row mb-5">
          <div class="col-md-6 mb-2">
            <label for="area" class="form-label">المنطقة</label>
            <input type="text" class="form-control" id="area" v-model="area">
          </div>
          <div class="col-md-6">
            <label for="city" class="form-label">المركز / المحافظة</label>
            <input type="text" class="form-control" id="city" v-model="city">
          </div>
        </div>

        <h5 class="mb-5 text-center">الباقة المطلوبة</h5>
        <div class="row mb-5">
          <div class="col-md-6">
            <label for="backage" class="form-label">اختر الباقة <span class="required">*</span></label>
            <input type="number" class="form-control" id="backage" v-model="backage" required>
          </div>
        </div>

        <div class="next row justify-content-center mb-4 mx-0">
          <div class="col-md-9 p-0">
            <button class="py-2" @click="updateStep(2)">التالي</button>
          </div>
        </div>
      </div>

      <!-- Step Two -->
      <div v-show="step == 2" class="step-two">
        <h5 class="mt-1 mb-5 text-center">بيانات المسؤلين</h5>
        <div class="row mb-5">
          <div class="col-md-6 mb-2">
            <label for="name" class="form-label">اسم المسؤل <span class="required">*</span></label>
            <input type="text" class="form-control" id="name" v-model="name" required>
          </div>
          <div class="col-md-6">
            <label for="position" class="form-label">منصبه <span class="required">*</span></label>
            <input type="text" class="form-control" id="position" v-model="position" required>
          </div>
        </div>

        <div class="row mb-5">
          <div class="col-md-6">
            <label>رقم الجوال</label>
            <div class="international-num d-flex position-relative pointer mt-2">
              <div class="country d-flex align-items-center" @click="countrySelectors.one=true">
                <span>{{ checkSelectedResponsableCountry.code }}</span>
                <img :src="require(`../assets/flags/${checkSelectedResponsableCountry.name}.gif`)" :alt="checkSelectedResponsableCountry.name">
              </div>
              <div v-show="countrySelectors.one" class="countries-list">
                <div v-for="country in countries" :key="country.code" class="countryCode d-flex align-items-center p-2" @click.stop="selectCountry(country)">
                  <span>{{ country.code }}</span>
                  <img :src="require(`../assets/flags/${country.name}.gif`)" :alt="country.name">
                </div>
              </div>
              <input type="tel" class="form-control" v-model="selectedResponsibleCountry.tel">
            </div>
          </div>
        </div>

        <div class="row mb-5">
          <div class="col-md-6 mb-2">
            <label for="contactAgentName" class="form-label">اسم المفوض بالتواصل <span class="required">*</span></label>
            <input type="text" class="form-control" id="contactAgentName" v-model="contactAgentName" required>
          </div>
          <div class="col-md-6">
            <label for="contactAgentPosition" class="form-label">منصبه<span class="required">*</span></label>
            <input type="text" class="form-control" id="contactAgentPosition" v-model="contactAgentPosition" required>
          </div>
        </div>

        <div class="row mb-5">
          <div class="col-md-6 mb-2">
            <label>رقم الجوال</label>
            <div class="international-num d-flex position-relative pointer mt-2">
              <div class="country d-flex align-items-center" @click="countrySelectors.two=true">
                <span>{{ checkSelectedContactAgent.code }}</span>
                <img :src="require(`../assets/flags/${checkSelectedContactAgent.name}.gif`)" :alt="checkSelectedContactAgent.name">
              </div>
              <div v-show="countrySelectors.two" class="countries-list">
                <div v-for="country in countries" :key="country.code" class="countryCode d-flex align-items-center p-2" @click.stop="selectContactAgentCountry(country)">
                  <span>{{ country.code }}</span>
                  <img :src="require(`../assets/flags/${country.name}.gif`)" :alt="country.name">
                </div>
              </div>
              <input type="tel" class="form-control" v-model="contactAgentCountry.tel">
            </div>
          </div>
          <div class="col-md-6">
            <label for="email" class="form-label">البريد الالكتروني <span class="required">*</span></label>
            <input type="email" class="form-control" id="email" v-model="email" required>
          </div>
        </div>

        <div class="row mb-5">
          <div class="col-md-12">
            <label for="notes" class="form-label">ملاحظات</label>
            <textarea class="form-control" id="notes" rows="5" v-model="notes"></textarea>
          </div>
        </div>

        <div class="submit-btn row justify-content-center mb-4 mx-0">
          <div class="col-md-9 p-0">
            <button class="py-2" @click="sendData">طلب المنتج</button>
          </div>
        </div>
      </div>

      <!-- Steps Indecators -->
      <div class="steps-selectors text-center mb-5">
        <button :class="step == 1? 'active':''" @click="updateStep(1)"></button>
        <button :class="step == 2? 'active':''" @click="updateStep(2)"></button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      step: 1,
      country: null,
      countries: [
        { name: 'bahrain', code: '+973'},
        { name: 'egypt', code: '+20'},
        { name: 'jordan', code: '+962'},
        { name: 'libya', code: '+218'},
        { name: 'morocco', code: '+212'},
        { name: 'palestinian_territory', code: '+970'},
        { name: 'qatar', code: '+974'},
        { name: 'saudi_arabia', code: '+966'},
        { name: 'sudan', code: '+249'},
        { name: 'syria', code: '+963'},
        { name: 'tunisia', code: '+216'},
        { name: 'turkey', code: '+90'},
        { name: 'yemen', code: '+967'},
      ],
      countrySelectors: {"one": false, "two": false},
      organizeName: null,
      organizeActivity: null,
      area: null,
      city: null,
      backage: null,
      name: null,
      position: null,
      selectedResponsibleCountry: {name: null, code: null, tel: null},
      contactAgentName: null,
      contactAgentPosition: null,
      contactAgentCountry: {name: null, code: null, tel: null},
      email: null,
      notes: null
    }
  },
  computed: {
    checkSelectedResponsableCountry() {
      return this.selectedResponsibleCountry.code? this.selectedResponsibleCountry : this.countries[0];
    },
    checkSelectedContactAgent() {
      return this.contactAgentCountry.code? this.contactAgentCountry : this.countries[0];
    }
  },
  methods: {
    updateStep(step) {
      this.step = step;
    },
    selectCountry(country) {
      this.selectedResponsibleCountry.name = country.name;
      this.selectedResponsibleCountry.code = country.code;
      this.countrySelectors.one = false;
    },
    selectContactAgentCountry(country) {
      this.contactAgentCountry.name = country.name;
      this.contactAgentCountry.code = country.code;
      this.countrySelectors.two = false;
    },
    sendData() {
      let data = new FormData();
      data.organizeName= this.organizeName;
      data.organizeActivity= this.organizeActivity;
      data.area= this.area;
      data.city= this.city;
      data.backage= this.backage;
      data.name= this.name;
      data.position= this.position;
      data.contactAgentName= this.contactAgentName;
      data.contactAgentPosition= this.contactAgentPosition;
      data.contactAgentCountry= this.contactAgentCountry;
      data.email= this.email;
      data.notes= this.notes;
      data.selectedResponsibleCountry= this.selectedResponsibleCountry;
      console.log(data);
    }
  }
}
</script>

<style lang="scss">
  h5 {
    color: #66BDE1;
  }
  label {
    color: gray;
  }
  .step-one {
    .next {
      button {
        width: 100%;
        height: 100%;
        border: none;
        color: white;
        background-color: #66BDE1;
      }
    }
  }
  .step-two {
    .international-num {
      .country {
        margin-left: 1.5rem;
        border: 1px solid #ced4da;
        background-color: #efefef;
        span {
          width: 40%;
          margin: 0 10px;
        }
        img {
          width: 30px;
          height: 20px;
          margin-left: 8px;
        }
      }
      .countries-list {
        position: absolute;
        height: 200px;
        overflow-y: scroll;
        background-color: #ccc;
        .countryCode {
          width: 120px;
          border-bottom: 1px solid #ced4da;
          span {
            width: 40%;
            margin: 0 10px;
          }
          img {
            width: 30px;
            height: 20px;
          }
        }
      }
    }
    .submit-btn {
      button {
        width: 100%;
        height: 100%;
        border: none;
        color: white;
        background-color: #66BDE1;
      }
    }
  }
  .steps-selectors {
    button {
      width: 15px;
      height: 15px;
      margin: 0 5px;
      border: none;
      border-radius: 50%;
      background-color: #999999;
      &.active {
        background-color: #66BDE1;
      }
    }
  }
</style>