# Gamra Model v3: Community-Centered Resort Framework

**Artifact ID:** `e7565995-2046-4f82-8d08-e1f18014b364`
**Source:** https://claude.ai/public/artifacts/e7565995-2046-4f82-8d08-e1f18014b364
**Filename:** `gamra-model-v3.jsx`
**Type:** `application/vnd.ant.react`

**Description:** Interactive visual framework for sustainable community tourism. Explore 5 operational layers, 2 cross-cutting systems, and impact models for cultural heritage preservation and local economic development.

---

## Source Code

```jsx
import { useState, useEffect, useRef } from "react";

// ═══ TOKENS ═══
const C = {
  bg: "#FAFAF7", card: "#FFFFFF", navy: "#1A2744", navyMid: "#2D4168",
  gold: "#B69D5F", goldSoft: "#C9B377", goldBg: "#F7F3EA",
  text: "#2F3542", textMid: "#5A6275", textSoft: "#8E95A4",
  green: "#4A8B6E", blue: "#4A6FA5", coral: "#C47259", purple: "#7B6B9E",
  border: "#EBE7DF", line: "#D6D0C4",
};

const FONT = "'Noto Sans Arabic', sans-serif";
const FONT_EN = "'DM Sans', sans-serif";
const FONT_DISPLAY = "'Playfair Display', serif";

// ═══ DATA ═══
const LAYERS_DATA = [
  { id:"L1", n:"١", ar:"الحوكمة والتنظيم", en:"Governance", color:C.navy, q:"من يفعل ماذا؟ ومن يمثّل المجتمع؟",
    summary:"Mantis لا تعمل مع أفراد — دائماً عبر شريك مؤسسي. نحن نبني نفس المنطق: كيان مجتمعي مستقل يملكه أهل المنطقة.",
    items:[
      {t:"تجمّع أثر قمرة",d:"كيان مستقل يمثّل المجتمع — جمعية تعاونية يملكها أهل المنطقة. يكتشف الكفاءات، ينظّم العلاقة مع المنتجع، يوزّع العوائد.",fx:"ضمان استقلالية المجتمع وصوته في القرار",how:"تأسيس جمعية أو فرع من جمعية الدار التراثية القائمة",cost:"منخفض"},
      {t:"المنسّق الميداني",d:"جسر بشري بين التجمّع وإدارة المنتجع. يُعيّن من أبناء المنطقة ويُدرّب على معايير Mantis.",fx:"تواصل يومي سلس بين عالمين مختلفين",how:"توظيف وتدريب شخص من المجتمع المحلي",cost:"منخفض"},
      {t:"بنية القرار والمعايير",d:"معايير جودة، آلية تسعير شفافة، نظام تقييم دوري، خطة تطوير سنوية مشتركة بين المنتجع والتجمّع.",fx:"استدامة الجودة وعدالة التوزيع",how:"ورش عمل مشتركة لوضع المعايير",cost:"منخفض"},
    ]},
  { id:"L2", n:"٢", ar:"رأس المال", en:"Capital Building", color:C.green, q:"ماذا نملك في الباحة؟ وكيف نستثمره؟",
    summary:"خمسة أنواع من رأس المال المحلي نحتاج اكتشافها وتوثيقها وتأهيلها: بشري وثقافي وطبيعي واقتصادي ومؤسسي.",
    items:[
      {t:"بشري — الناس",d:"حرفيات الخصف، حائكات الجبّة، نحّالون، طبّاخات، رواة وشعراء شقر، مرشدون.",fx:"قاعدة كفاءات حيّة جاهزة للتفعيل",how:"مسح ميداني + تقييم + برامج تأهيل في الضيافة والسلامة",cost:"متوسط"},
      {t:"ثقافي — المعرفة",d:"الشقر والجناس، العرضة والمسحباني، لهجة غامد وزهران الفصيحة، العمارة الحجرية، المطبخ، قصص القبائل.",fx:"مكتبة ثقافية رقمية تحمي التراث وتغذّي التجارب",how:"توثيق صوتي ومرئي + أرشفة رقمية",cost:"متوسط"},
      {t:"طبيعي — الأرض",d:"المزارع المدرّجة، غابات السروات، نباتات طبية، فواكه جبلية (موز وريحان وكادي)، مسارات مشي.",fx:"خريطة أصول طبيعية قابلة للتحويل لتجارب",how:"مسح بيئي + تصميم مسارات",cost:"متوسط"},
      {t:"اقتصادي — المنتجات",d:"العسل الجبلي، سعفيات وخصف، سوق الثلاثاء، الجبّة الصوفية، ملابس مطرّزة.",fx:"سلاسل توريد محلية جاهزة",how:"تقييم + رفع جودة + تغليف يناسب الضيف",cost:"متوسط-مرتفع"},
      {t:"مؤسسي — الشبكات",d:"جمعية الدار التراثية، تعاونيات، جامعة الباحة، هيئة التراث، الروابط القبلية.",fx:"شبكة شراكات تُسرّع التنفيذ",how:"بناء علاقات + مذكرات تفاهم",cost:"منخفض"},
    ]},
  { id:"L3", n:"٣", ar:"المنتج المجتمعي", en:"Community Product", color:C.blue, q:"كيف نحوّل رأس المال إلى تجارب؟",
    summary:"أربعة أنماط تغطّي كل طبقات التجربة — من ما يحسّه الضيف دون أن يدري إلى ما يبقى أثره بعد سنوات.",
    items:[
      {t:"المدمج — ما لا يُرى لكنه يُحَس",d:"منسوج في نسيج المنتجع: أعمال فنية، روائح ريحان وكادي، عناصر عمارة حجرية، عسل ترحيبي، أبيات شقر، ألحان الجنوب.",fx:"هوية مكانية فريدة + عقود توريد = دخل ثابت للمجتمع",how:"تكليف حرفيين بعناصر التصميم الداخلي + عقود توريد دورية",cost:"مرتفع أولاً ثم منخفض"},
      {t:"المبرمج — ما يختاره الضيف",d:"تجارب قابلة للحجز: ورش خصف وبخور وتطريز، طبخ محلي، حلقات رواة، تربية نحل، جلسات شعرية حيّة.",fx:"أجور مباشرة لمقدّمي التجارب + تفاعل عميق",how:"تصميم ٥-٨ تجارب + تدريب مقدّميها + نظام حجز",cost:"متوسط"},
      {t:"الممتد — ما يأخذ الضيف للمجتمع",d:"رحلات خارج المنتجع: ذي عين، المزارع المدرّجة والقطف، سوق الثلاثاء، مسارات مشي، ضيافة بيتية.",fx:"إنفاق مباشر في المجتمع + تجربة لا تُكرر",how:"تصميم مسارات + تأهيل مواقع + مرشدون محليون",cost:"متوسط"},
      {t:"الدائم — ما يبقى بعد الرحيل",d:"صندوق أثر الضيف، منح صغيرة، تدريب شباب، توثيق تراث، حاضنة ريادة أعمال مجتمعية.",fx:"تنمية مستدامة + حفظ تراث + محتوى Mantis Impact",how:"تصميم آليات صناديق ومنح + شراكات مؤسسية",cost:"مرتفع — عائد طويل المدى"},
    ]},
  { id:"L4", n:"٤", ar:"قنوات التوصيل", en:"Delivery", color:C.coral, q:"أين يلتقي المجتمع بالضيف؟",
    summary:"نقاط تماس مصمّمة بعناية داخل المنتجع وخارجه — كل قناة مربوطة بنمط من أنماط المنتج المجتمعي.",
    items:[
      {t:"داخل المنتجع — خمس مساحات",d:"نبض المكان (التفاصيل الثقافية)، مطبخ قمرة (المطعم كتجربة)، ساحة الورش (التفاعل)، مجلس القصص (الشعر والحكايات)، متجر المحلّي (المنتجات).",fx:"الضيف يعيش الثقافة دون أن يغادر",how:"تصميم المساحات ضمن مخطط المنتجع + تشغيل يومي",cost:"مدمج في التشغيل"},
      {t:"خارج المنتجع — خمس وجهات",d:"الدروب (مسارات)، القرى (ذي عين)، المزارع (حصاد وقطف)، الأسواق (سوق الثلاثاء)، البيوت (ضيافة محلية حقيقية).",fx:"الإنفاق يصل مباشرة + تجربة لا يقدّمها منافس",how:"اتفاقيات مع مواقع + نقل + مرشدون",cost:"متوسط"},
    ]},
  { id:"L5", n:"٥", ar:"الأثر والتبادل", en:"Impact", color:C.purple, q:"ماذا يكسب كل طرف؟",
    summary:"القيمة لا تتدفق في اتجاه واحد — كل طرف يعطي ويحصل. هذا نموذج أعمال مستدام لا مشروع خيري.",
    items:[
      {t:"الضيف",d:"تجربة أصيلة، ارتباط عاطفي بإنسان ومكان، قصص يحملها معه، شعور بأنه صنع فرقاً حقيقياً.",fx:"ولاء عميق + رغبة بالعودة + تسويق شفهي",how:"تصميم كل نقطة تماس عبر نموذج رحلة الضيف",cost:"—"},
      {t:"المجتمع",d:"دخل مباشر، تطوير مهارات، حفظ تراث وهوية، فرص عمل، كيان مؤسسي يمثّله ويحمي مصالحه.",fx:"تنمية اقتصادية واجتماعية وثقافية متكاملة",how:"عبر الطبقات الخمس مجتمعة",cost:"—"},
      {t:"المشغّل — Mantis",d:"محتوى Impact أصيل، تمايز تنافسي، ولاء ضيوف أعلى، قصص تسويقية لا تُشترى.",fx:"توافق كامل مع فلسفة ومعايير Mantis",how:"كل نموذج مصمّم على أركان Mantis",cost:"—"},
      {t:"المنطقة — الباحة",d:"نموذج مستدام قابل للتكرار، توثيق منهجي، تنمية متوازنة، هوية كوجهة ثقافية.",fx:"تحوّل من وجهة طبيعية إلى ثقافية-طبيعية",how:"نموذج القياس والتقارير الدورية",cost:"—"},
    ]},
];

const SYSTEMS_DATA = [
  { id:"S1", ar:"نظام الارتباط", en:"The Bond System", color:C.green, icon:"◆",
    q:"يحوّل الضيف من زائر عابر إلى شريك مرتبط بإنسان وقصة ومشروع",
    summary:"يخترق كل طبقة — الشخصيات مسجّلة في التجمّع (حوكمة)، موثّقة (رأس مال)، مُفعّلة (منتج)، مُوصلة (قنوات)، مُقاسة (أثر).",
    items:[
      {t:"الغرفة = القصة",d:"كل غرفة تحمل اسماً من ثقافة المنطقة، وكتيّب قصة، وعملاً فنياً أصلياً، وقضية تنموية، وكبسولة صوتية بصوت الشخصية.",fx:"الغرفة بوابة علاقة لا مكان نوم",how:"تصميم ٣٠ قصة + كتيّبات + أعمال فنية + تسجيل صوتي",cost:"متوسط — مرة واحدة"},
      {t:"الرفيق المحلي",d:"ليس مرشداً بل رفيق إقامة — يطبخ ويمشي ويحكي. اختياري بسعر شفاف: الضيف يعرف كم يصل للرفيق وكم يذهب للصندوق.",fx:"تجربة إنسانية لا يقدّمها أي فندق",how:"اختيار ١٠-١٥ شخصية + تدريب مكثف + جدولة",cost:"أجور بالتجربة"},
      {t:"الاستثمار الأصغر",d:"يُتاح للضيف المساهمة (٥٠٠-٥٠٠٠ ريال) في مشروع الشخصية عبر منصة رقمية شفافة مع متابعة.",fx:"علاقة مستمرة بعد المغادرة + سبب للعودة",how:"منصة بسيطة + آلية متابعة + تقارير",cost:"متوسط — تطوير تقني"},
      {t:"التقويم الموسمي",d:"القصة تتغير مع الموسم — حصاد الموز في أبريل، الريحان في يونيو، العسل في أغسطس، الجبّة في الشتاء.",fx:"كل زيارة مختلفة + دافع للعودة",how:"تقويم سنوي + تحديث محتوى الغرف",cost:"منخفض"},
    ]},
  { id:"S2", ar:"نظام الحواس", en:"The Senses System", color:C.gold, icon:"✦",
    q:"يصمّم كل نقطة تماس حسّياً — هوية حسّية موحّدة مبنية على الباحة",
    summary:"يخترق كل طبقة — المعايير الحسّية (حوكمة)، الأصول مصنّفة (رأس مال)، التجارب مصمّمة حسّياً (منتج)، القنوات تُفعّل الحواس (توصيل)، الذاكرة الحسّية (أثر).",
    items:[
      {t:"السمع — ألحان وشعر",d:"ألحان العرضة والمسحباني كموسيقى محيطة، كبسولات صوتية، شعر شقر حي، مسابقة كلمات لهجة غامد وزهران.",fx:"الضيف يسمع الباحة — اللغة والإيقاع",how:"تسجيلات احترافية + نظام صوتي + مسابقة تفاعلية",cost:"متوسط"},
      {t:"البصر — فن وعمارة",d:"أعمال فنية من أبيات الشقر، عمارة حجرية مدمجة، زي الموظفين من الجبّة التقليدية، إضاءة دافئة.",fx:"هوية بصرية لا تُنسى ولا تُقلّد",how:"تكليف فنانين + تعاون معماري + تصميم أزياء",cost:"مرتفع — جزء من التصميم"},
      {t:"الشمّ — ريحان وكادي",d:"توقيع عطري من الريحان البلدي، كادي طازج في الغرف، صابون أعشاب محلية، بخور السدر مساءً.",fx:"ذاكرة شمّية — أقوى أنواع الذاكرة الإنسانية",how:"تطوير منتجات مع حرفيين + نظام عطري",cost:"متوسط"},
      {t:"الذوق — عسل ومحصول",d:"عسل وقهوة عند الوصول، فطور موسمي، قائمة حكاية المحصول، القطف باليد.",fx:"الأكل تجربة كاملة الدورة لا مجرد وجبة",how:"شراكات مزارعين + قائمة موسمية + تجربة القطف",cost:"مدمج في المطعم"},
      {t:"اللمس — حجر ونسيج",d:"أقمشة بتقنيات محلية، حجر طبيعي حقيقي، هدايا خصف وسعفيات، المادة الخام في الورش.",fx:"الضيف يلمس المكان حرفياً",how:"توريد مواد محلية + تصميم هدايا + تجهيز ورش",cost:"متوسط"},
    ]},
];

// ═══ DETAIL PANEL ═══
const DetailPanel = ({ data, onClose }) => {
  if (!data) return null;
  const c = data.color || C.navy;
  return (
    <div onClick={onClose} style={{ position:"fixed", inset:0, zIndex:9000, display:"flex", justifyContent:"flex-end" }}>
      <div style={{ position:"absolute", inset:0, background:"rgba(26,39,68,0.18)", backdropFilter:"blur(4px)" }} />
      <div onClick={e=>e.stopPropagation()} style={{
        position:"relative", width:"min(680px, 80vw)", background:C.card, overflowY:"auto",
        boxShadow:"-4px 0 60px rgba(0,0,0,0.12)", animation:"panelIn 0.3s ease",
      }}>
        <style>{`@keyframes panelIn{from{transform:translateX(100%);opacity:0}to{transform:translateX(0);opacity:1}}`}</style>
        
        {/* Header */}
        <div style={{ position:"sticky", top:0, zIndex:2, background:C.card, borderBottom:`1px solid ${C.border}`, padding:"20px 36px", display:"flex", alignItems:"center", justifyContent:"space-between" }}>
          <button onClick={onClose} style={{ background:C.bg, border:`1px solid ${C.border}`, borderRadius:8, padding:"6px 14px", cursor:"pointer", fontFamily:FONT, fontSize:12, color:C.textMid }}>✕</button>
          <div style={{ textAlign:"right", direction:"rtl" }}>
            <h2 style={{ fontFamily:FONT, color:C.navy, fontSize:22, fontWeight:700, margin:0 }}>{data.ar}</h2>
            <p style={{ fontFamily:FONT_EN, color:c, fontSize:11, letterSpacing:1.5, textTransform:"uppercase", margin:0 }}>{data.en}</p>
          </div>
        </div>

        <div style={{ padding:"28px 36px", direction:"rtl" }}>
          {/* Core question */}
          <div style={{ padding:"18px 22px", background:`${c}08`, borderRadius:14, borderRight:`3px solid ${c}`, marginBottom:28 }}>
            <p style={{ fontFamily:FONT, color:C.navy, fontSize:16, fontWeight:600, marginBottom:6 }}>{data.q}</p>
            <p style={{ fontFamily:FONT, color:C.text, fontSize:14, lineHeight:2 }}>{data.summary}</p>
          </div>

          {/* Items */}
          {data.items?.map((item, i) => (
            <div key={i} style={{ marginBottom:20, background:C.bg, borderRadius:16, padding:24, border:`1px solid ${C.border}` }}>
              <div style={{ display:"flex", alignItems:"center", gap:10, marginBottom:12 }}>
                <div style={{ width:28, height:28, borderRadius:8, background:`${c}12`, display:"flex", alignItems:"center", justifyContent:"center", fontSize:13, fontWeight:700, color:c, fontFamily:FONT_EN, flexShrink:0 }}>{i+1}</div>
                <h4 style={{ fontFamily:FONT, color:C.navy, fontSize:15, fontWeight:700, margin:0 }}>{item.t}</h4>
              </div>
              <p style={{ fontFamily:FONT, color:C.text, fontSize:13.5, lineHeight:2.1, marginBottom:14 }}>{item.d}</p>
              <div style={{ display:"grid", gridTemplateColumns:"1fr 1fr 1fr", gap:8 }}>
                {[
                  {label:"الأثر المتوقع", val:item.fx, bg:"#E8F5EE", ac:C.green},
                  {label:"طريقة التنفيذ", val:item.how, bg:"#EBF0F7", ac:C.blue},
                  {label:"التكلفة", val:item.cost, bg:"#FBF0EC", ac:C.coral},
                ].map((m,j) => (
                  <div key={j} style={{ padding:"10px 12px", borderRadius:10, background:m.bg }}>
                    <p style={{ fontFamily:FONT, fontSize:10, color:m.ac, fontWeight:700, marginBottom:3, letterSpacing:0.3 }}>{m.label}</p>
                    <p style={{ fontFamily:FONT, fontSize:12, color:C.text, lineHeight:1.7, margin:0 }}>{m.val}</p>
                  </div>
                ))}
              </div>
            </div>
          ))}
        </div>
      </div>
    </div>
  );
};

// ═══ MAIN ═══
export default function App() {
  const [panel, setPanel] = useState(null);
  const [lens, setLens] = useState("model");
  const mapRef = useRef(null);

  const Section = ({ children, dark }) => (
    <section style={{
      minHeight:"100vh", display:"flex", flexDirection:"column", alignItems:"center", justifyContent:"center",
      padding:"100px 40px", position:"relative", background: dark ? C.goldBg : C.bg,
    }}>{children}</section>
  );

  const Chip = ({ children }) => (
    <div style={{ display:"inline-block", padding:"6px 18px", borderRadius:24, background:`${C.gold}14`, border:`1px solid ${C.gold}30`, fontFamily:FONT, fontSize:12, fontWeight:500, color:C.gold, marginBottom:20 }}>{children}</div>
  );

  const LayerRow = ({ layer, onClick }) => (
    <div onClick={onClick} style={{
      display:"flex", alignItems:"center", gap:20, padding:"18px 24px",
      background:C.card, borderRadius:14, border:`1.5px solid ${layer.color}20`,
      cursor:"pointer", transition:"all 0.25s", direction:"rtl",
    }}
    onMouseEnter={e=>{e.currentTarget.style.borderColor=layer.color+"60";e.currentTarget.style.boxShadow=`0 4px 20px ${layer.color}12`;e.currentTarget.style.transform="translateX(-4px)"}}
    onMouseLeave={e=>{e.currentTarget.style.borderColor=layer.color+"20";e.currentTarget.style.boxShadow="none";e.currentTarget.style.transform="none"}}
    >
      <div style={{ width:44, height:44, borderRadius:12, background:`${layer.color}10`, border:`1.5px solid ${layer.color}25`, display:"flex", alignItems:"center", justifyContent:"center", fontFamily:FONT, fontSize:20, fontWeight:700, color:layer.color, flexShrink:0 }}>{layer.n}</div>
      <div style={{ flex:1 }}>
        <h4 style={{ fontFamily:FONT, color:C.navy, fontSize:16, fontWeight:700, marginBottom:2 }}>{layer.ar}</h4>
        <p style={{ fontFamily:FONT, color:C.textMid, fontSize:13, margin:0 }}>{layer.q}</p>
      </div>
      <div style={{ display:"flex", flexDirection:"column", alignItems:"flex-start", flexShrink:0 }}>
        <span style={{ fontFamily:FONT_EN, color:`${layer.color}88`, fontSize:10, letterSpacing:1.5, textTransform:"uppercase" }}>{layer.en}</span>
        <span style={{ fontFamily:FONT, color:layer.color, fontSize:12, marginTop:4 }}>← استكشف</span>
      </div>
    </div>
  );

  const SystemCard = ({ sys, onClick }) => (
    <div onClick={onClick} style={{
      background:C.card, borderRadius:16, padding:28, cursor:"pointer",
      border:`1px solid ${sys.color}20`, transition:"all 0.25s", direction:"rtl",
      position:"relative", overflow:"hidden",
    }}
    onMouseEnter={e=>{e.currentTarget.style.borderColor=sys.color+"50";e.currentTarget.style.boxShadow=`0 6px 28px ${sys.color}12`}}
    onMouseLeave={e=>{e.currentTarget.style.borderColor=sys.color+"20";e.currentTarget.style.boxShadow="none"}}
    >
      <div style={{ position:"absolute", top:0, right:0, width:80, height:80, background:`${sys.color}06`, borderRadius:"0 0 0 80px" }} />
      <span style={{ fontSize:22, display:"block", marginBottom:12 }}>{sys.icon}</span>
      <h3 style={{ fontFamily:FONT, color:C.navy, fontSize:18, fontWeight:700, marginBottom:4 }}>{sys.ar}</h3>
      <p style={{ fontFamily:FONT_EN, color:sys.color, fontSize:10, letterSpacing:1.5, textTransform:"uppercase", marginBottom:12 }}>{sys.en}</p>
      <p style={{ fontFamily:FONT, color:C.textMid, fontSize:13, lineHeight:2 }}>{sys.q}</p>
      <div style={{ marginTop:14, padding:"8px 14px", background:`${sys.color}08`, borderRadius:8, display:"inline-block" }}>
        <span style={{ fontFamily:FONT, fontSize:12, color:sys.color, fontWeight:500 }}>اضغط للتفاصيل ←</span>
      </div>
    </div>
  );

  const MANTIS = [
    { title:"حفظ الثقافة والتراث", en:"Conservation & Culture", color:C.blue,
      desc:"حماية وإحياء الموروث من خلال دمجه في التجربة",
      refs:[
        {label:"نموذج الحواس — الهوية الحسّية", target:SYSTEMS_DATA[1]},
        {label:"المنتج المدمج — الثقافة في كل زاوية", target:LAYERS_DATA[2]},
        {label:"رأس المال الثقافي — التوثيق", target:LAYERS_DATA[1]},
      ]},
    { title:"تنمية المجتمع", en:"Community Development", color:C.green,
      desc:"بناء قدرات المجتمع وتمكينه اقتصادياً ومؤسسياً",
      refs:[
        {label:"نموذج الارتباط — من ضيف إلى شريك", target:SYSTEMS_DATA[0]},
        {label:"الحوكمة — التجمّع المجتمعي", target:LAYERS_DATA[0]},
        {label:"الأثر والتبادل — القيمة المتبادلة", target:LAYERS_DATA[4]},
      ]},
    { title:"الاستدامة", en:"Sustainability", color:C.gold,
      desc:"ضمان أن الأثر مستدام وقابل للقياس والتكرار",
      refs:[
        {label:"المنتج الدائم — الصناديق والمنح", target:LAYERS_DATA[2]},
        {label:"التبادل الاقتصادي — ٥ تدفقات", target:LAYERS_DATA[4]},
        {label:"قنوات التوصيل — سلاسل التوريد", target:LAYERS_DATA[3]},
      ]},
  ];

  return (
    <div style={{ fontFamily:FONT, color:C.text, background:C.bg }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Noto+Sans+Arabic:wght@300;400;500;600;700;800&family=DM+Sans:wght@300;400;500;600&display=swap');
        *{margin:0;padding:0;box-sizing:border-box}
        html{scroll-behavior:smooth}
        ::-webkit-scrollbar{width:5px}
        ::-webkit-scrollbar-track{background:${C.bg}}
        ::-webkit-scrollbar-thumb{background:${C.gold}44;border-radius:4px}
      `}</style>

      {/* ══════ 1. THE GATEWAY ══════ */}
      <Section>
        <div style={{ textAlign:"center", maxWidth:600 }}>
          <p style={{ fontFamily:FONT_EN, color:C.gold, fontSize:11, letterSpacing:5, textTransform:"uppercase", marginBottom:48 }}>ASFAR · MANTIS · AZR STUDIO</p>
          <div style={{ width:48, height:1.5, background:`linear-gradient(90deg, transparent, ${C.gold}, transparent)`, margin:"0 auto 40px" }} />
          
          <h1 style={{ fontFamily:FONT, color:C.navy, fontSize:52, fontWeight:800, lineHeight:1.4, marginBottom:8 }}>نموذج التشابك</h1>
          <p style={{ fontFamily:FONT_DISPLAY, color:C.gold, fontSize:24, fontStyle:"italic", marginBottom:48 }}>The Interlocking Model</p>

          <div style={{ padding:"36px 44px", background:C.card, borderRadius:20, border:`1px solid ${C.border}`, boxShadow:"0 8px 40px rgba(0,0,0,0.04)", position:"relative" }}>
            <div style={{ position:"absolute", top:-16, right:40, background:C.bg, padding:"6px 16px" }}>
              <span style={{ fontFamily:FONT_DISPLAY, color:C.gold, fontSize:32, fontStyle:"italic" }}>❝</span>
            </div>
            <p style={{ fontFamily:FONT, color:C.navy, fontSize:24, lineHeight:2.4, fontWeight:700, direction:"rtl" }}>
              المنتجع ليس المنتج<br/>الباحة هي المنتج<br/>المنتجع هو البوابة
            </p>
          </div>

          <p style={{ fontFamily:FONT, color:C.textSoft, fontSize:14, marginTop:36, direction:"rtl", lineHeight:2 }}>
            منتجع قمرة · الباحة · ٣٠ جناحاً · ارتفاع ٢٢٦٠م · أبريل ٢٠٢٦
          </p>
        </div>
      </Section>

      {/* ══════ 2. AL-BAHA ══════ */}
      <Section dark>
        <div style={{ maxWidth:760, textAlign:"center" }}>
          <Chip>الكنز</Chip>
          <h2 style={{ fontFamily:FONT, color:C.navy, fontSize:38, fontWeight:700, marginBottom:10, direction:"rtl" }}>الباحة — أرض لم تُكتشف بعد</h2>
          <p style={{ fontFamily:FONT, color:C.textMid, fontSize:15, lineHeight:2.2, marginBottom:40, direction:"rtl" }}>
            قبيلتا غامد وزهران · تراث يمتد لأكثر من ألفي عام · ومنها خرج الخليل بن أحمد الفراهيدي — مخترع علم العروض
          </p>
          <div style={{ display:"grid", gridTemplateColumns:"repeat(3,1fr)", gap:16, direction:"rtl" }}>
            {[
              {icon:"𝄞",t:"فن الشقر",d:"شعر ارتجالي قائم على الجناس — تشابه الألفاظ واختلاف المعاني، فن لغوي فريد عالمياً"},
              {icon:"⬡",t:"٤٠٠٠+ برج حجري",d:"عمارة متدرّجة شاهدة على عبقرية البناء والتكيّف مع جغرافيا السروات"},
              {icon:"◈",t:"العسل الجبلي",d:"تقليد نحل يعود لأجيال — مهرجان عسل دولي سنوي يستقطب الآلاف"},
              {icon:"◉",t:"الجبّة الصوفية",d:"ثوب تقليدي يُحاك ويُطرّز يدوياً على مدى أشهر — تحفة ملبوسة"},
              {icon:"◐",t:"قرية ذي عين",d:"قرية أثرية عمرها ٤٠٠+ سنة على قائمة اليونسكو المؤقتة — رخام أبيض فوق جبل"},
              {icon:"◭",t:"الريحان والكادي",d:"مزارع مدرّجة فريدة تنتج فواكه وأعشاباً جبلية لا توجد في مكان آخر"},
            ].map((c,i) => (
              <div key={i} style={{ background:C.card, borderRadius:16, padding:"24px 20px", border:`1px solid ${C.border}`, textAlign:"right" }}>
                <div style={{ width:40, height:40, borderRadius:10, background:C.goldBg, display:"flex", alignItems:"center", justifyContent:"center", fontFamily:FONT_EN, fontSize:18, color:C.gold, marginBottom:12 }}>{c.icon}</div>
                <h4 style={{ fontFamily:FONT, color:C.navy, fontSize:15, fontWeight:700, marginBottom:6 }}>{c.t}</h4>
                <p style={{ fontFamily:FONT, color:C.textMid, fontSize:12.5, lineHeight:1.9 }}>{c.d}</p>
              </div>
            ))}
          </div>
        </div>
      </Section>

      {/* ══════ 3. THE FRAMEWORK ══════ */}
      <Section>
        <div style={{ maxWidth:660, textAlign:"center" }}>
          <Chip>الإطار</Chip>
          <h2 style={{ fontFamily:FONT, color:C.navy, fontSize:38, fontWeight:700, marginBottom:10 }}>البنية الكاملة</h2>
          <p style={{ fontFamily:FONT, color:C.textMid, fontSize:15, lineHeight:2.2, marginBottom:40, direction:"rtl" }}>
            خمس طبقات تشغيلية يخترقها نظامان عابران
            <br/>كل طبقة تبني على التي تحتها — لا يمكن تقديم منتج بلا رأس مال، ولا رأس مال بلا حوكمة
          </p>

          {/* Visual diagram */}
          <div style={{ display:"grid", gridTemplateColumns:"1fr 3fr 1fr", gap:14, alignItems:"stretch", direction:"rtl" }}>
            {/* Right system */}
            <div style={{ background:`${C.green}06`, border:`1.5px solid ${C.green}18`, borderRadius:16, padding:"20px 14px", display:"flex", flexDirection:"column", alignItems:"center", justifyContent:"center", gap:8 }}>
              <span style={{ fontSize:20 }}>◆</span>
              <p style={{ fontFamily:FONT, fontSize:13, fontWeight:700, color:C.green, textAlign:"center" }}>نظام<br/>الارتباط</p>
              <div style={{ width:1, flex:1, background:`${C.green}25`, margin:"4px 0" }} />
              <p style={{ fontFamily:FONT_EN, fontSize:9, color:C.green, letterSpacing:1 }}>BOND</p>
            </div>

            {/* Center layers */}
            <div style={{ display:"flex", flexDirection:"column", gap:8 }}>
              {LAYERS_DATA.map((l,i) => (
                <div key={i} style={{
                  display:"flex", alignItems:"center", gap:12, padding:"14px 20px",
                  background:C.card, borderRadius:12, border:`1px solid ${l.color}18`, direction:"rtl",
                }}>
                  <span style={{ fontFamily:FONT, fontSize:20, fontWeight:800, color:l.color }}>{l.n}</span>
                  <span style={{ fontFamily:FONT, fontSize:14, fontWeight:600, color:C.navy }}>{l.ar}</span>
                  <span style={{ marginRight:"auto", fontFamily:FONT_EN, fontSize:10, color:C.textSoft, letterSpacing:1, textTransform:"uppercase" }}>{l.en}</span>
                </div>
              ))}
            </div>

            {/* Left system */}
            <div style={{ background:`${C.gold}08`, border:`1.5px solid ${C.gold}18`, borderRadius:16, padding:"20px 14px", display:"flex", flexDirection:"column", alignItems:"center", justifyContent:"center", gap:8 }}>
              <span style={{ fontSize:20 }}>✦</span>
              <p style={{ fontFamily:FONT, fontSize:13, fontWeight:700, color:C.gold, textAlign:"center" }}>نظام<br/>الحواس</p>
              <div style={{ width:1, flex:1, background:`${C.gold}25`, margin:"4px 0" }} />
              <p style={{ fontFamily:FONT_EN, fontSize:9, color:C.gold, letterSpacing:1 }}>SENSES</p>
            </div>
          </div>
        </div>
      </Section>

      {/* ══════ 4. SYSTEMS ══════ */}
      <Section dark>
        <div style={{ maxWidth:720 }}>
          <div style={{ textAlign:"center", marginBottom:40 }}>
            <Chip>الابتكار</Chip>
            <h2 style={{ fontFamily:FONT, color:C.navy, fontSize:36, fontWeight:700, marginBottom:10 }}>النظامان العابران</h2>
            <p style={{ fontFamily:FONT, color:C.textMid, fontSize:14, lineHeight:2.2, direction:"rtl" }}>
              ليسا "مخرجات" بل <strong style={{color:C.navy}}>أنظمة تشغيلية</strong> تخترق كل مستوى من الحوكمة إلى القياس
            </p>
          </div>
          <div style={{ display:"grid", gridTemplateColumns:"1fr 1fr", gap:20 }}>
            {SYSTEMS_DATA.map(s => <SystemCard key={s.id} sys={s} onClick={()=>setPanel(s)} />)}
          </div>
        </div>
      </Section>

      {/* ══════ 5. LAYERS ══════ */}
      <Section>
        <div style={{ maxWidth:640 }}>
          <div style={{ textAlign:"center", marginBottom:40 }}>
            <Chip>البنية التشغيلية</Chip>
            <h2 style={{ fontFamily:FONT, color:C.navy, fontSize:36, fontWeight:700, marginBottom:10 }}>الطبقات الخمس</h2>
            <p style={{ fontFamily:FONT, color:C.textMid, fontSize:14, lineHeight:2.2, direction:"rtl" }}>
              اضغط على أي طبقة لاستكشاف عناصرها بالتفصيل — التوصيف والأثر وطريقة التنفيذ والتكلفة
            </p>
          </div>
          <div style={{ display:"flex", flexDirection:"column", gap:10 }}>
            {LAYERS_DATA.map((l,i) => (
              <div key={i}>
                <LayerRow layer={l} onClick={()=>setPanel(l)} />
                {i<4 && <div style={{ textAlign:"center", padding:"3px 0", color:C.line, fontSize:16 }}>↓</div>}
              </div>
            ))}
          </div>
        </div>
      </Section>

      {/* ══════ 6. MANTIS ══════ */}
      <Section dark>
        <div style={{ maxWidth:820 }}>
          <div style={{ textAlign:"center", marginBottom:40 }}>
            <Chip>التوافق</Chip>
            <h2 style={{ fontFamily:FONT, color:C.navy, fontSize:36, fontWeight:700, marginBottom:6 }}>أركان Mantis الثلاثة</h2>
            <p style={{ fontFamily:FONT_DISPLAY, color:C.gold, fontSize:16, fontStyle:"italic", marginBottom:16 }}>"Man And Nature Together Is Sustainable"</p>
            <p style={{ fontFamily:FONT, color:C.textMid, fontSize:14, lineHeight:2, direction:"rtl" }}>
              كل ركن مغطّى بنماذج فرعية تفصيلية — اضغط على أي عنصر للانتقال لتفاصيله
            </p>
          </div>
          <div style={{ display:"grid", gridTemplateColumns:"1fr 1fr 1fr", gap:20, direction:"rtl" }}>
            {MANTIS.map((p,i) => (
              <div key={i} style={{ background:C.card, borderRadius:18, overflow:"hidden", border:`1px solid ${C.border}` }}>
                <div style={{ padding:"22px 22px 16px", borderBottom:`1px solid ${C.border}`, background:`${p.color}05` }}>
                  <p style={{ fontFamily:FONT_EN, color:p.color, fontSize:10, letterSpacing:2, textTransform:"uppercase", marginBottom:8 }}>{p.en}</p>
                  <h3 style={{ fontFamily:FONT, color:C.navy, fontSize:17, fontWeight:700, marginBottom:8 }}>{p.title}</h3>
                  <p style={{ fontFamily:FONT, color:C.textMid, fontSize:12.5, lineHeight:1.9 }}>{p.desc}</p>
                </div>
                <div style={{ padding:"14px 18px", display:"flex", flexDirection:"column", gap:6 }}>
                  {p.refs.map((r,j) => (
                    <button key={j} onClick={()=>setPanel(r.target)} style={{
                      background:C.bg, border:`1px solid ${p.color}15`, borderRadius:10,
                      padding:"10px 14px", cursor:"pointer", textAlign:"right", width:"100%",
                      fontFamily:FONT, fontSize:12.5, color:C.text, lineHeight:1.7,
                      transition:"all 0.2s",
                    }}
                    onMouseEnter={e=>{e.currentTarget.style.borderColor=p.color+"50";e.currentTarget.style.background=`${p.color}06`}}
                    onMouseLeave={e=>{e.currentTarget.style.borderColor=p.color+"15";e.currentTarget.style.background=C.bg}}
                    >
                      <span>{r.label}</span>
                      <span style={{ float:"left", color:p.color, fontSize:11 }}>←</span>
                    </button>
                  ))}
                </div>
              </div>
            ))}
          </div>
        </div>
      </Section>

      {/* ══════ 7. NUMBERS ══════ */}
      <Section>
        <div style={{ maxWidth:600, textAlign:"center" }}>
          <Chip>بالأرقام</Chip>
          <h2 style={{ fontFamily:FONT, color:C.navy, fontSize:34, fontWeight:700, marginBottom:10, direction:"rtl" }}>لماذا هذا النموذج فريد؟</h2>
          <div style={{ display:"grid", gridTemplateColumns:"repeat(4,1fr)", gap:20, margin:"36px 0" }}>
            {[{n:"٥",l:"طبقات تشغيلية"},{n:"٢",l:"نظام عابر"},{n:"٧",l:"نموذج فرعي"},{n:"٣٠+",l:"عنصر تفصيلي"}].map((s,i) => (
              <div key={i}>
                <div style={{ fontFamily:FONT, fontSize:36, fontWeight:800, color:C.gold }}>{s.n}</div>
                <div style={{ fontFamily:FONT, fontSize:12, color:C.textSoft, marginTop:4 }}>{s.l}</div>
              </div>
            ))}
          </div>
          <div style={{ display:"flex", flexDirection:"column", gap:8, direction:"rtl", textAlign:"right", maxWidth:480, margin:"0 auto" }}>
            {[
              "ليست أفكار بل نظام متشابك — كل نموذج مرتبط بالآخر",
              "مبنية من داخل ثقافة الباحة — الشقر والخصف وغامد وزهران",
              "متوافقة بنيوياً مع أركان Mantis Impact الثلاثة",
              "تحوّل الضيف من زائر إلى شريك ومستثمر حقيقي",
              "كل ريال شفاف — التدفقات مكشوفة بالكامل",
              "قابلة للتكرار في منتجعات أسفار الأخرى",
            ].map((d,i) => (
              <div key={i} style={{ display:"flex", gap:10, alignItems:"flex-start", padding:"10px 0" }}>
                <span style={{ color:C.gold, fontSize:14, marginTop:4, flexShrink:0 }}>✓</span>
                <p style={{ fontFamily:FONT, fontSize:14, color:C.text, lineHeight:1.9 }}>{d}</p>
              </div>
            ))}
          </div>
        </div>
      </Section>

      {/* ══════ FOOTER ══════ */}
      <footer style={{ padding:"48px 0", textAlign:"center", background:C.bg, borderTop:`1px solid ${C.border}` }}>
        <div style={{ width:40, height:1.5, background:`linear-gradient(90deg, transparent, ${C.gold}, transparent)`, margin:"0 auto 20px" }} />
        <p style={{ fontFamily:FONT_EN, color:C.textSoft, fontSize:11, letterSpacing:3 }}>
          GAMRA RESORT · AL-BAHA · THE INTERLOCKING MODEL
        </p>
        <p style={{ fontFamily:FONT_EN, color:C.line, fontSize:10, letterSpacing:2, marginTop:8 }}>AZR STUDIO © 2026</p>
      </footer>

      {/* ══════ PANEL ══════ */}
      <DetailPanel data={panel} onClose={()=>setPanel(null)} />
    </div>
  );
}
```
