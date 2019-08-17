
# 代码集合

## 获取官方页面录取名单表格

```javascript
var tbody = $('table').children[0].children
var man = 0;
var woman = 0;
var content = ''

Array.from(tbody).forEach(tr => {
  var text = '| '
  Array.from(tr.children).forEach(td=>{
    if(tr.children[0]===td) return
    if (td.innerText==='男'){
      man += 1;
    } else if (td.innerText === '女'){
      woman += 1
    }
    text += td.innerText + ' | '
  })
  content += text + '\n'
});
console.log(content)
console.log(`男：${man} 女${woman}`)
```

## 获取各个专业人数男女比例

```js
var content = {}
var data = document.getElementsByTagName('tr');
Array.from(data).forEach(tr => {
  let zhuanye = tr.children[3].innerText;
  if(zhuanye === '录取专业') return
  let sex = tr.children[2].innerText;
  if (!content[zhuanye]) {
    content[zhuanye] = {
      man: 0,
      woman: 0,
    }
  }
  if (sex === '男') {
    content[zhuanye].man += 1
  } else {
    content[zhuanye].woman += 1
  }
})
function toPercent(point) {
  let str = Number(point * 100).toFixed(2);
  str += "%";
  return str;
}

var contentText = ''
var allContent = [0,0]
for (key in content){
  let text = `- ${key}\n`
  let man = content[key].man;
  allContent[0] += man;
  let woman = content[key].woman;
  allContent[1] += woman;
  let all = content[key].man + content[key].woman;
  text += `\t- 男: ${man} 人，占 ${toPercent(man / all)}\n`
  text += `\t- 女: ${woman} 人，占 ${toPercent(woman / all)}\n`
  text += `\t- 合计: ${all}\n`
  contentText += text
}
console.log(`${contentText}
- 合计:\n\t- 男: ${allContent[0]} 人，占 ${toPercent(allContent[0] / (allContent[0] + allContent[1]))}\n\t- 女: ${allContent[1]} 人，占 ${toPercent(allContent[1] / (allContent[0] + allContent[1]))}\n\t - 合计: ${ allContent[0] + allContent[1] }\n
`)
```

## 获取地区分布

```js
var codejson = {
    "name": "山西省", "zip": "140000",
    "city": [
        {
            "name": "太原市", "zip": "140100",
            "county": [
                { "name": "市辖区", "zip": "140101" },
                { "name": "小店区", "zip": "140105" },
                { "name": "迎泽区", "zip": "140106" },
                { "name": "杏花岭区", "zip": "140107" },
                { "name": "尖草坪区", "zip": "140108" },
                { "name": "万柏林区", "zip": "140109" },
                { "name": "晋源区", "zip": "140110" },
                { "name": "清徐县", "zip": "140121" },
                { "name": "阳曲县", "zip": "140122" },
                { "name": "娄烦县", "zip": "140123" },
                { "name": "古交市", "zip": "140181" }
            ]
        },
        {
            "name": "大同市", "zip": "140200",
            "county": [
                { "name": "市辖区", "zip": "140201" },
                { "name": "城区", "zip": "140202" },
                { "name": "矿区", "zip": "140203" },
                { "name": "南郊区", "zip": "140211" },
                { "name": "新荣区", "zip": "140212" },
                { "name": "阳高县", "zip": "140221" },
                { "name": "天镇县", "zip": "140222" },
                { "name": "广灵县", "zip": "140223" },
                { "name": "灵丘县", "zip": "140224" },
                { "name": "浑源县", "zip": "140225" },
                { "name": "左云县", "zip": "140226" },
                { "name": "大同县", "zip": "140227" }
            ]
        },
        {
            "name": "阳泉市", "zip": "140300",
            "county": [
                { "name": "市辖区", "zip": "140301" },
                { "name": "城区", "zip": "140302" },
                { "name": "矿区", "zip": "140303" },
                { "name": "郊区", "zip": "140311" },
                { "name": "平定县", "zip": "140321" },
                { "name": "盂县", "zip": "140322" }
            ]
        },
        {
            "name": "长治市", "zip": "140400",
            "county": [
                { "name": "市辖区", "zip": "140401" },
                { "name": "城区", "zip": "140402" },
                { "name": "郊区", "zip": "140411" },
                { "name": "长治县", "zip": "140421" },
                { "name": "襄垣县", "zip": "140423" },
                { "name": "屯留县", "zip": "140424" },
                { "name": "平顺县", "zip": "140425" },
                { "name": "黎城县", "zip": "140426" },
                { "name": "壶关县", "zip": "140427" },
                { "name": "长子县", "zip": "140428" },
                { "name": "武乡县", "zip": "140429" },
                { "name": "沁县", "zip": "140430" },
                { "name": "沁源县", "zip": "140431" },
                { "name": "潞城市", "zip": "140481" }
            ]
        },
        {
            "name": "晋城市", "zip": "140500",
            "county": [
                { "name": "晋城市市辖区", "zip": "140501" },
                { "name": "城区", "zip": "140502" },
                { "name": "沁水县", "zip": "140521" },
                { "name": "阳城县", "zip": "140522" },
                { "name": "陵川县", "zip": "140524" },
                { "name": "泽州县", "zip": "140525" },
                { "name": "高平市", "zip": "140581" }
            ]
        },
        {
            "name": "朔州市", "zip": "140600",
            "county": [
                { "name": "市辖区", "zip": "140601" },
                { "name": "朔城区", "zip": "140602" },
                { "name": "平鲁区", "zip": "140603" },
                { "name": "山阴县", "zip": "140621" },
                { "name": "应县", "zip": "140622" },
                { "name": "右玉县", "zip": "140623" },
                { "name": "怀仁县", "zip": "140624" }
            ]
        },
        {
            "name": "晋中市", "zip": "140700",
            "county": [
                { "name": "市辖区", "zip": "140701" },
                { "name": "榆次区", "zip": "140702" },
                { "name": "榆社县", "zip": "140721" },
                { "name": "左权县", "zip": "140722" },
                { "name": "和顺县", "zip": "140723" },
                { "name": "昔阳县", "zip": "140724" },
                { "name": "寿阳县", "zip": "140725" },
                { "name": "太谷县", "zip": "140726" },
                { "name": "祁县", "zip": "140727" },
                { "name": "平遥县", "zip": "140728" },
                { "name": "灵石县", "zip": "140729" },
                { "name": "介休市", "zip": "140781" }
            ]
        },
        {
            "name": "运城市", "zip": "140800",
            "county": [
                { "name": "市辖区", "zip": "140801" },
                { "name": "盐湖区", "zip": "140802" },
                { "name": "临猗县", "zip": "140821" },
                { "name": "万荣县", "zip": "140822" },
                { "name": "闻喜县", "zip": "140823" },
                { "name": "稷山县", "zip": "140824" },
                { "name": "新绛县", "zip": "140825" },
                { "name": "绛县", "zip": "140826" },
                { "name": "垣曲县", "zip": "140827" },
                { "name": "夏县", "zip": "140828" },
                { "name": "平陆县", "zip": "140829" },
                { "name": "芮城县", "zip": "140830" },
                { "name": "永济市", "zip": "140881" },
                { "name": "河津市", "zip": "140882" }
            ]
        },
        {
            "name": "忻州市", "zip": "140900",
            "county": [
                { "name": "市辖区", "zip": "140901" },
                { "name": "忻府区", "zip": "140902" },
                { "name": "定襄县", "zip": "140921" },
                { "name": "五台县", "zip": "140922" },
                { "name": "代县", "zip": "140923" },
                { "name": "繁峙县", "zip": "140924" },
                { "name": "宁武县", "zip": "140925" },
                { "name": "静乐县", "zip": "140926" },
                { "name": "神池县", "zip": "140927" },
                { "name": "五寨县", "zip": "140928" },
                { "name": "岢岚县", "zip": "140929" },
                { "name": "河曲县", "zip": "140930" },
                { "name": "保德县", "zip": "140931" },
                { "name": "偏关县", "zip": "140932" },
                { "name": "原平市", "zip": "140981" }
            ]
        },
        {
            "name": "临汾市", "zip": "141000",
            "county": [
                { "name": "市辖区", "zip": "141001" },
                { "name": "尧都区", "zip": "141002" },
                { "name": "曲沃县", "zip": "141021" },
                { "name": "翼城县", "zip": "141022" },
                { "name": "襄汾县", "zip": "141023" },
                { "name": "洪洞县", "zip": "141024" },
                { "name": "古县", "zip": "141025" },
                { "name": "安泽县", "zip": "141026" },
                { "name": "浮山县", "zip": "141027" },
                { "name": "吉县", "zip": "141028" },
                { "name": "乡宁县", "zip": "141029" },
                { "name": "大宁县", "zip": "141030" },
                { "name": "隰县", "zip": "141031" },
                { "name": "永和县", "zip": "141032" },
                { "name": "蒲县", "zip": "141033" },
                { "name": "汾西县", "zip": "141034" },
                { "name": "侯马市", "zip": "141081" },
                { "name": "霍州市", "zip": "141082" }
            ]
        },
        {
            "name": "吕梁市", "zip": "141100",
            "county": [
                { "name": "市辖区", "zip": "141101" },
                { "name": "离石区", "zip": "141102" },
                { "name": "文水县", "zip": "141121" },
                { "name": "交城县", "zip": "141122" },
                { "name": "兴县", "zip": "141123" },
                { "name": "临县", "zip": "141124" },
                { "name": "柳林县", "zip": "141125" },
                { "name": "石楼县", "zip": "141126" },
                { "name": "岚县", "zip": "141127" },
                { "name": "方山县", "zip": "141128" },
                { "name": "中阳县", "zip": "141129" },
                { "name": "交口县", "zip": "141130" },
                { "name": "孝义市", "zip": "141181" },
                { "name": "汾阳市", "zip": "141182" }
            ]
        }
    ]
};

var content = [];
function getCity(code) {
  codejson.city.forEach((v, key) => {
    if (!content[key]) {
      content[key] = {
        name: v.name,
        value: 0,
        county: []
      }
    }
    v.county.forEach((area, aKey) => {
      if (!content[key].county[aKey]){
        content[key].county[aKey] = {
          name: area.name,
          value: 0
        }
      }
      let areaCode = code.split('').slice(2, 8).join('');
      if (area.zip === areaCode) {
        content[key].county[aKey].value += 1;
        content[key].value += 1;
      }
    })
  })
}

var data = document.getElementsByTagName('tr');
Array.from(data).forEach(tr => {
  let stdCode = tr.children[0].innerText;
  getCity(String(stdCode))
})

var contentText = ''
content.forEach(v=>{
  let text = `- ${v.name}: ${v.value} 人\n`
  v.county.forEach(a=>{
    if(a.value!==0){
      text += `\t - ${a.name}: ${a.value} 人\n`
    }
  })
  contentText += text;
})
```
