<template>
  <div id="app">
    <div class="col-lg-12 querybuilder-control">
      <ejs-querybuilder
        id="querybuilder"
        ref="querybuilder"
        :actionBegin="actionBegin"
        width="70%"
      >
        <e-columns>
          <e-column
            field="IndexField"
            label="IndexField"
            type="string"
            :ruleTemplate="menuTemplate"
          />
          <e-column
            field="CompanyId"
            label="CompanyId"
            type="string"
            :ruleTemplate="menuTemplate"
          />
          <e-column
            field="Status"
            label="Status"
            type="string"
            :ruleTemplate="menuTemplate"
          />
          <e-column
            field="Total"
            label="Total"
            type="string"
            :ruleTemplate="menuTemplate"
          />
        </e-columns>
      </ejs-querybuilder>
    </div>
  </div>
</template>

<style>
.e-query-builder {
  margin: 0 auto;
}
</style>

<script>
import Vue from "vue";
import { QueryBuilderPlugin } from "@syncfusion/ej2-vue-querybuilder";
import { DropDownListPlugin } from "@syncfusion/ej2-vue-dropdowns";
import { MenuPlugin } from "@syncfusion/ej2-vue-navigations";
import { getComponent, compile } from "@syncfusion/ej2-base";

Vue.use(QueryBuilderPlugin);
Vue.use(DropDownListPlugin);
Vue.use(MenuPlugin);
export default {
  data: function () {
    return {
      menuTemplate: () => {
        return {
          template: Vue.component("ruleTemplate", {
            template: `<div class="e-rule e-rule-template">
                        <div class="e-rule-filter e-custom-filter">
                       <div class="e-input-group">
                
        <input class="e-input" name='input' type="text" v-bind:id='inputID' :value='data.rule.field'/>
          <ejs-menu :items='menuItems' v-bind:id='valueID' v-on:select="selectMenu($event, valueID)"></ejs-menu>
  </div>
                        </div>
                            <div class="e-rule-operator e-operator">
                                 <ejs-dropdownlist :change='operatorChange' :dataSource="operators" :fields='fields' :value='data.rule.operator'>
                            </ejs-dropdownlist>
                            </div>
                            <div class="e-rule-value e-value">
                             <input class="e-input" type="text" v-on:keyup="onKeyPressBtwn" />
                             </div>
                            <div class="e-rule-btn e-rule-value-delete">
                                <button class="e-removerule e-rule-delete e-css e-btn e-small e-round">
                                    <span class="e-btn-icon e-icons e-delete-icon"/>
                                </button>
                            </div>
                        
                    </div>`,
            data(args) {
              return {
                qryBldrObj: getComponent(
                  document.getElementById("querybuilder"),
                  "query-builder"
                ),
              };
            },
            computed: {
              operators: function () {
                return [
                  { key: "Equal", value: "equal" },
                  { key: "Not equal", value: "notequal" },
                  { key: "Greater than", value: "greaterthan" },
                  { key: "Less than", value: "lessthan" },
                  { key: "Less than or equal", value: "lessthanorequal" },
                  { key: "Greater than or equal", value: "greaterthanorequal" },
                ];
              },
              fields: function () {
                return { text: "key", value: "value" };
              },
              menuItems: function () {
                return [
                     { iconCss: "", 
                      items: [
                          { text: "IndexField",  items: [
                          { text: "CompanyId" },
                          { text: "Status" },
                          { text: "Total" },
                        ] }
                        ]}
                ];
              },
              valueID: function () {
                return `${this.data.ruleID}_menuId`;
              },
              inputID: function () {
                return `${this.data.ruleID}_inputId`;
              },
            },
            methods: {
              fieldChange: function (args) {
                this.qryBldrObj.notifyChange(args.value, args.element, "field");
              },
              operatorChange: function (args) {
                this.qryBldrObj.notifyChange(
                  args.value,
                  args.element,
                  "operator"
                );
              },
              selectMenu: function(args, id) {
                if (args.item.text!="") {
                   var element = document.getElementById(id.split("menuId")[0]+"inputId");
                    element.value=args.item.text;
                   this.qryBldrObj.notifyChange(args.item.text, element, "field");
                }
                   
              },
               onKeyPressBtwn: function(args) {
                   this.qryBldrObj.notifyChange(args.target.value, args.target, "value");
               },
            },
          }),
        };
      },
    };
  },
  methods: {
    actionBegin: function (args) {
     
    },
  },
};
</script>

<style>
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-dropdowns/styles/material.css";
@import "../node_modules/@syncfusion/ej2-inputs/styles/material.css";
@import "../node_modules/@syncfusion/ej2-lists/styles/material.css";
@import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
@import "../node_modules/@syncfusion/ej2-navigations/styles/material.css";
@import "../node_modules/@syncfusion/ej2-calendars/styles/material.css";
@import "../node_modules/@syncfusion/ej2-vue-querybuilder/styles/material.css";
.e-query-builder {
  margin: 0 auto;
}
.e-input-group-icon.e-ddl-icon:before {
content: '\E969';
font-family: 'e-icons';
  }
</style>