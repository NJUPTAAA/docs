# FrontEnd Utils

## alert()
Pop up an alert box with a confirmation button
```javascript
alert(content, title, icon, backdrop)
```
### params
content:
   * **type:** string
   * **default:** undefined
   * **description:** title of alert box

title:
   * **type:** string
   * **default:** "Notice"
   * **description:** content of alert box

icon:
   * **type:** string
   * **default:** "information-outline"
   * **description:** the class name of the alert box's icon

backdrop:
   * **type:** string | boolean
   * **default:** "static"
   * **description:** enable box close
### example

```javascript
alert('content','title','information-outline',true)
```

### explanation

None

### availability

Accessible since 0.2.3

***

## confirm()
Pop up a confirm box with done&deny button
```javascript
confirm({params},callback(deny))
```
### params
content:
   * **type:** string
   * **default:** undefined
   * **description:** title of alert box

title:
   * **type:** string
   * **default:** "Notice"
   * **description:** content of alert box

icon:
   * **type:** string
   * **default:** "information-outline"
   * **description:** the class name of the alert box's icon

backdrop:
   * **type:** string | boolean
   * **default:** "static"
   * **description:** enable box close

### callback(deny)
deny:
   * **type:** boolean
   * **description:** true means deny, false means done

### example

```javascript
confirm({
    content:'content',
    title:'title',
    icon:'information-outline',
    backdrop:true
},function(deny){
    if(deny){
        console.log('deny');
    }
    else{
        console.log('done');
    }
})
```
### explanation

None

### availability

Accessible since 0.2.3

***

## prompt()
Pop up a prompt box with done&deny button
```javascript
prompt({params},callback(deny,text))
```
### params
content:
   * **type:** string
   * **default:** undefined
   * **description:** title of alert box

title:
   * **type:** string
   * **default:** "Notice"
   * **description:** content of alert box

placeholder:
   * **type:** string
   * **default:** "Input Field"
   * **description:** the placeholder of input

value:
   * **type:** string
   * **default:** undefined
   * **description:** the value of input

icon:
   * **type:** string
   * **default:** "information-outline"
   * **description:** the class name of the alert box's icon

backdrop:
   * **type:** string | boolean
   * **default:** "static"
   * **description:** enable box close
### callback
deny:
   * **type:** boolean
   * **description:** true means deny, false means done

text:
   * **type:** string
   * **description:** the input text  
### example

```javascript
prompt({
    content:'Please tell us your name.',
    title:'Your Name',
    placeholder:"write down your name",
    icon:'information-outline',
    backdrop:true
},function(deny,text){
    if(!deny){
        console.log(`you are ${text},done`)
    }
    else{
        console.log(`you are ${text},deny`)
    }
})

```
### explanation

param text is the value of the input component

### availability

Accessible since 0.2.3


## notify()
pop up global notification
```javascript
notify(title,body,icon,tag){
```
1. title:
   * type: string
   * default: undefined
   * description: the title of notification
2. body:
   * type: string
   * default: undefined
   * description: the body of the notification
4. icon:
   * type: string
   * default: "/static/img/njupt.png"
   * description: the path of icon
5. tag:
   * type: string
   * default: "default"
   * description: the tag of notification
### example

```javascript
notify("Welcome",'Hi, welcome back to the Fully new NOJ',"/static/img/notify/njupt.png",'welcome');

```
### explanation

None

### availability

Accessible since 0.2.3