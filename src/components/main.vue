<template lang="pug">
  div#left-section
    div.innerLeft
      h1 {{msg}}
      hr
      b-tabs
        b-tab(title="Input" active)
          div.section-container
            b-form(@submit='onSubmit', @reset='onReset', v-if='show')
              draggable( class="dragArea", :options="{group:{ name:'elem',  pull:'clone', put:'true' }}" )
                b-form-group#exampleInputGroup1(label='Email address:', label-for='exampleInput1', description="We'll never share your email with anyone else.")
                  b-form-input#exampleInput1(type='email', v-model='form.email', required='', placeholder='Enter email')
                b-form-group#exampleInputGroup2(label='Your Name:', label-for='exampleInput2')
                  b-form-input#exampleInput2(type='text', v-model='form.name', required='', placeholder='Enter name')
                b-form-group#exampleInputGroup3(label='Food:', label-for='exampleInput3')
                  b-form-select#exampleInput3(:options='foods', required='', v-model='form.food')
                b-form-group#exampleGroup4
                  b-form-checkbox-group#exampleChecks(v-model='form.checked')
                    b-form-checkbox(value='me') Check me out
                    b-form-checkbox(value='that') Check that out
                b-button(type='submit', variant='primary') Submit
                b-button(type='reset', variant='danger') Reset
        b-tab(title="Radios / Checkboxes")
          div.section-container
            b-form-checkbox-group#checkboxes2(name='flavour2', v-model='selected' label='Form Checkboxes')
              draggable( class="dragArea", :options="{group:{ name:'elem',  pull:'clone', put:false }}" )
                b-form-checkbox(value='orange') Orange
                b-form-checkbox(value='apple') Apple
                b-form-checkbox(value='pineapple') Pineapple
                b-form-checkbox(value='grape') Grape
            div
              | Selected:
              strong {{ selected }}
            hr
            b-form-group(label="Radios using sub-components")
              b-form-radio-group#radios2(v-model='selectedCheck', name='radioSubComponent')
                draggable( class="dragArea", :options="{group:{ name:'elem',  pull:'clone', put:false }}" )
                  b-form-radio(value='first') Toggle this custom radio
                  b-form-radio(value='second') Or toggle this other custom radio
                  b-form-radio(value='third', disabled='') This one is Disabled
                  b-form-radio(:value='{fourth: 4}') This is the 4th radio
              div
                | Selected:
                strong {{ selectedCheck }}
              hr
        b-tab(title="Select" )
          div.section-container
            draggable( class="dragArea", :options="{group:{ name:'elem',  pull:'clone', put:false }}" )
              b-form-select.mb-3(v-model='selected')
                option(:value='null') Please select an option
                option(value='a') Option A
                option(value='b', disabled='') Option B (disabled)
                optgroup(label='Grouped Options')
                option(:value="{'C':'3PO'}") Option with object value
                option(:value="{'R':'2D2'}") Another option with object value
            div
              | Selected:
              strong {{ selected }}
            hr
            draggable( class="dragArea", :options="{group:{ name:'elem',  pull:'clone', put:false }}" )
              b-form-select.mb-3(v-model='selected', :options='options', :select-size='4')
            div
        b-tab(title="View HTML", @click="getHtml")
          div
            textarea#txtArea.html-view {{txtArea}}
        b-tab(title="About" )
          div.about.section-container
            h1 About
            p Created By Adam Moore (@minikomi) to help take the stress out of writing all that markup to get bootstrap forms together. The original version of this was a big jQuery spaghetti mess, so as of March 2013 it has been rewritten using backbone.js and takes advantage of underscode.js templates.
            p If you have a problem, or want a specific snippet added please check out the github project. Note, this is only a simple tool so I'm not that keen on adding many features (eg. saving/exporting forms, embedding forms etc.).
            p Adding snippets is quite simple now (due to the rewrite!) so please don't hesitate to open an issue!
    div.right-form
      h1 {{headerRight}}
      hr
      div
        form#formHtml(@click="getHtml")
          draggable.field-right.dragArea(:options="{group:'elem', pull:'false' }")
            fieldset
</template>

<script>

// Imported Css
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

// Imported modules
import Vue from 'vue'
import VueDraggable from 'vue-draggable'
import BootstrapVue from 'bootstrap-vue'
import draggable from 'vuedraggable'

// Usage module
Vue.use(BootstrapVue)
Vue.use(VueDraggable)

export default {
  name: 'HelloWorld',
  props: ['htmlForm'],
  data () {
    return {
      headerRight: 'Your Form',
      form: {
        email: '',
        name: '',
        food: null,
        checked: []
      },
      foods: [
        { text: 'Select One', value: null },
        'Carrots', 'Beans', 'Tomatoes', 'Corn'
      ],
      show: true,
      txtArea: null,
      selected: [], // Must be an array reference!
      options: [
        {text: 'Orange', value: 'orange'},
        {text: 'Apple', value: 'apple'},
        {text: 'Pineapple', value: 'pineapple'},
        {text: 'Grape', value: 'grape'}
      ],
      selectedCheck: 'first',
      optionsCheck: [
        { text: 'Toggle this custom radio', value: 'first' },
        { text: 'Or toggle this other custom radio', value: 'second' },
        { text: 'This one is Disabled', value: 'third', disabled: true },
        { text: 'This is the 4th radio', value: {fourth: 4} }
      ],
      optionsDrag: {
        dropzoneSelector: '.right-form fieldset',
        draggableSelector: 'form div',
        excludeOlderBrowsers: true,
        multipleDropzonesItemsDraggingEnabled: true,
        showDropzoneAreas: true,
        // onDrop: function(event) {},
        // onDragstart: function(event) {},
        // onDragend: function(event) {},
        nativeEvent: {}, // native js event
        items: [], // list of selected draggable elements
        owner: null, // old dropzone element
        droptarget: null // new dropzone element
      },
      msg: 'Drag & Drop components'
    }
  },
  components: {
    draggable
  },
  created: function () {
    //
  },
  methods: {
    onSubmit (evt) {
      evt.preventDefault()
      alert(JSON.stringify(this.form))
    },
    onReset (evt) {
      evt.preventDefault()
      /* Reset our form values */
      this.form.email = ''
      this.form.name = ''
      this.form.food = null
      this.form.checked = []
      /* Trick to reset/clear native browser form validation state */
      this.show = false
      this.$nextTick(() => { this.show = true })
    },
    getHtml () {
      console.log(this.$el)
      // window.jQuery('#formHtml').html()
      this.txtArea = document.getElementById('formHtml').outerHTML
      // console.log(this.txtArea)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #left-section{
    display: flex;
  }
  .section-container{
    margin: 30px 10px 0px 20px;
  }
  .about{
    text-align: left;
  }
  .html-view{
    margin: 20px 10px;
    border: 1px solid #ccc;
    min-height: 220px;
    padding: 5px;
    padding-bottom: 50px;
    width: 100%;
  }
  .right-form{
     flex: 1;
     margin: 0px 40px;
   }
  .field-right{
    border: 1px solid #ccc;
    min-height: 220px;
    padding: 5px;
    padding-bottom: 50px;
  }
  .innerLeft{
    flex: 1;
  }
  #left-section{
    width: 100%;
  }
</style>
