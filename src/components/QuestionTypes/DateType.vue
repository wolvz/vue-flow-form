<script>
  /*
    Copyright (c) 2020 - present, DITDOT Ltd. - MIT Licence
    https://github.com/ditdot-dev/vue-flow-form
    https://www.ditdot.hr/en
  */

  import TextType from './TextType.vue'
  import { QuestionType } from '../../models/QuestionModel'
  import LanguageModel from '../../models/LanguageModel'

  export default {
    extends: TextType,
    name: QuestionType.Date,
    data() {
      return {
        inputType: 'date'
      }
    }, 
    methods: {
      showInvalid() {
        return this.errorMessage !== null
      },
      validate() {
        let date = Date.parse(this.dataValue);

        if (this.question.min && date < this.question.min) {
          this.errorMessage = this.language.formatString(this.language.errorMinimumDate, {
            date: new Date(this.question.min.getTime() + 86400000).toISOString().substring(0, 10)
          })
          return false
        }

        if (this.question.max && date > this.question.max) {
          return false
        }

        if (this.question.required && !this.hasValue) {
          return false
        }

        this.errorMessage = null;

        return true
      }
    }
  }
</script>