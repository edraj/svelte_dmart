<script>
  import {QueryType} from "@edraj/tsdmart";
  import ListView from "@/lib/ListView.svelte";
</script>

# عرض القائمة

يمكنك الآن إجراء بحث عن النص الكامل أو بحث يعتمد على السمات لهذا الحقل.
على سبيل المثال، لنفترض أننا نريد استرداد جميع المجلدات الفرعية ضمن مساحة **mysapce**

نحن نسمي واجهة برمجة التطبيقات `/query` بنص الطلب التالي

```json
{
  "filter_shortnames": [],
  "type": "subpath",
  "search": "",
  "space_name": "myspace",
  "subpath": "/",
  "exact_subpath": true,
  "limit": 15,
  "offset": 0,
  "retrieve_json_payload": true,
  "sort_type": "ascending",
  "sort_by": "created_at"
}
```

وستكون النتائج:

<ListView
type={QueryType.subpath}
space_name={"myspace"}
subpath={"/"}
scope={"public"}
/>


