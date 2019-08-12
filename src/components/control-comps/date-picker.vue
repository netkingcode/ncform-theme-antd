<template>
  <div>
    <a-date-picker class="ncform-date-picker"
      v-if="type === 'date'"
      :placeholder="placeholder || $nclang(typeOptions[type].placeholder)"
      :disabled="disabled || readonly"
      :allowClear="mergeConfig.clearable"
      v-show="!hidden"
      v-model="momentModelVal"
      :defaultValue="defaultValue" 
      >
    </a-date-picker>
  </div>
</template>

<style lang="scss">
  .h-layout {
    .ncform-date-picker {
      &.__ncform-control {
        clear: none;
      }
    }
  }

  .v-layout {
    .ncform-date-picker {
      &.__ncform-control {
        clear: both;
      }
    }
  }

  .ncform-date-picker {
    &.el-date-editor.el-input {
      width: 100%;
    }
  }
</style>

<script>
import ncformCommon from '@ncform/ncform-common';
import moment from 'moment';

const controlMixin = ncformCommon.mixins.vue.controlMixin;

export default {
  mixins: [controlMixin],

  i18nData: {
    en: {
      chYear: 'Choose Year',
      chMonth: 'Choose Month',
      chDate: 'Choose Date',
      chWeek: 'Choose Week',
      chTime: 'Choose Datetime',
      weekFormat: 'Week WW of yyyy'
    },
    zh_cn: {
      chYear: '选择年份',
      chMonth: '选择月份',
      chDate: '选择日期',
      chWeek: '选择周',
      chTime: '选择时间',
      weekFormat: 'yyyy年 第WW周'
    }
  },

  props: {
    value: {
      type: String,
      default: ''
    }
  },

  created() {
    this.$data.momentModelVal = this._convertValue(this.value)
    this.$data.defaultValue = this.$data.momentModelVal
    // console.log("==created")
    // console.log(this.value)
    // if (this.value) {
    //   this.$data.momentModelVal = moment(Number(this.value))
    // } else {
    //   this.$data.momentModelVal = null
    // }    
  },

  mounted() {
    if(this.$data.modelVal){
      // this.$data.modelVal = this.mergeConfig.valueFormat ? this.$data.modelVal : new Date(parseInt(this.$data.modelVal));
    }
  },

  data() {
    return {
      typeOptions: {
        year: {
          format: '',
          placeholder: 'chYear',
        },
        month: {
          format: '',
          placeholder: 'chMonth',
        },
        date: {
          format: '',
          placeholder: 'chDate',
        },
        week: {
          format: 'weekFormat',
          placeholder: 'chWeek',
        },
        datetime:{
          format: '',
          placeholder: 'chTime',
        }
      },
      // 组件特有的配置属性
      defaultConfig: {
        clearable: false,
        type: "date",  // year/month/date/week/datetime
        format: '',
        valueFormat: ''
      },
      // modelVal：请使用该值来绑定实际的组件的model
      momentModelVal: null,
      defaultValue: null      
    };
  },

  computed: {
    // defaultValue() {
    //   return this._convertValue(this.value)
    // },
    // disabled / readonly / hidden / placeholder 你可以直接使用这些变量来控制组件的行为
    type() {
      if(!this.$data.typeOptions[this.mergeConfig.type]){
        return 'date';
      } else {
        return this.mergeConfig.type;
      }
    }
  },

  watch: {
    momentModelVal(newVal) {
      const val = this._processMomentModelVal(newVal);
      // // this.$options.tempProcessedVal = val; // 用这个变量来记录处理过后的值，然后下面进行比较，避免循环
      // // this.$emit("input", val);
      this.$data.modelVal = val
      console.log("------")
      console.log(val)
    }
  },

  methods: {
    moment,
    // 你可以通过该方法在modelVal传出去之前进行加工处理，即在this.$emit('input')之前
    _processMomentModelVal(newVal){
      console.log("===")
      console.log(newVal.format())
      if (newVal) {
        return newVal.valueOf().toString()
      } else {
        return newVal
      }
      
      //return `${newVal ? (this.mergeConfig.valueFormat ? newVal : +new Date(newVal)) : ''}`;
    },
    _convertValue(val){
      if (!val) return null
      var parsedVal
      if (!this.mergeConfig.valueFormat || this.mergeConfig.valueFormat === 'timestamp') {
        parsedVal = moment(Number(val))   
      } else {
        parsedVal = moment(val)
      }
      return (parsedVal.isValid()) ? parsedVal : null
    }
  }
};
</script>
