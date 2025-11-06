/* تطبيق تمويل رصيد - نموذج أولي (Single-file React component) تعليمات: هذا ملف React جاهز للعرض داخل Canvas. يستخدم Tailwind CSS للستايل. يتضمن:

شاشة تسجيل دخول/تسجيل (محاكاة)

لوحة رئيسية تعرض الرصيد، عملية تعبئة رصيد مع خيار تمويل (قرض/دفع لاحق)

صفحة تاريخ المعاملات

مودال لخيارات التمويل (فترة سداد، فوائد افتراضية)

محاكاة استدعاءات API وبيانات وهمية


ملاحظة تقنية: هذا ملف عرض/نموذج أولي للواجهة الأمامية فقط. أسفل الكود يوجد ملحق يشرح API المطلوب وقاعدة البيانات والتكاملات المقترحة (مزود دفع، التحقق، حماية). */

import React, { useState, useEffect } from 'react';

export default function TopUpFinanceApp() { const [user, setUser] = useState(null); // {id, name, balance} const [screen, setScreen] = useState('auth'); // auth | dashboard | history const [loading, setLoading] = useState(false); const [transactions, setTransactions] = useState([]); const [showFinanceModal, setShowFinanceModal] = useState(false); const [topupAmount, setTopupAmount] = useState(''); const [selectedPlan, setSelectedPlan] = useState(null);

useEffect(() => { // محاكاة جلب البيانات - لو المستخدم مسجل بالفعل const saved = null; // وضعية demo: لا يوجد حفظ if (saved) { setUser(saved); setScreen('dashboard'); } }, []);

function mockLogin(name) { setLoading(true); setTimeout(() => { const u = { id: 'u123', name: name || 'مستخدم تجريبي', balance: 10.00 }; setUser(u); setTransactions([ { id: 't1', type: 'topup', amount: 10.0, date: '2025-11-01', method: 'دفع نقدي' } ]); setLoading(false); setScreen('dashboard'); }, 700); }

function handleTopUp() { const amount = parseFloat(topupAmount); if (!amount || amount <= 0) return alert('ادخل قيمة صحيحة'); // إظهار خيارات التمويل setShowFinanceModal(true); }

function confirmTopUp(financePlan) { setShowFinanceModal(false); setSelectedPlan(financePlan); setLoading(true); // محاكاة استدعاء API للدفع / إنشاء طلب تمويل setTimeout(() => { // إذا تم اختيار تمويل (credit) const isFinanced = financePlan && financePlan.type === 'finance'; const id = 'tx_' + Math.random().toString(36).slice(2,9); const tx = { id, type: isFinanced ? 'topup_financed' : 'topup', amount: parseFloat(topupAmount), date: new Date().toISOString().slice(0,10), method: isFinanced ? تمويل - ${financePlan.period} شهر : 'دفع فوري' }; setTransactions(prev => [tx, ...prev]); setUser(u => ({ ...u, balance: (u.balance + parseFloat(topupAmount)) })); setTopupAmount(''); setLoading(false); alert('تم تنفيذ العملية بنجاح'); }, 1200); }

function logout() { setUser(null); setScreen('auth'); setTransactions([]); }

if (screen === 'auth') { return ( <div className="min-h-screen flex items-center justify-center bg-gray-50 p-4"> <div className="max-w-md w-full bg-white rounded-2xl p-6 shadow"> <h1 className="text-2xl font-semibold mb-4">تسجيل الدخول - تطبيق تمويل رصيد</h1> <p className="text-sm text-gray-500 mb-4">جرب: اضغط "تسجيل دخول تجريبي" للانتقال للنموذج.</p> <button onClick={() => mockLogin('أحمد')} className="w-full py-2 rounded-xl bg-indigo-600 text-white font-medium"> {loading ? 'جاري التحميل...' : 'تسجيل دخول تجريبي'} </button> <div className="mt-4 text-center text-sm text-gray-400">أو اضف كتابة اسم مستخدم في المستقبل</div> </div> </div> ); }

return ( <div className="min-h-screen bg-gradient-to-br from-white to-gray-100 p-6"> <header className="max-w-3xl mx-auto flex items-center justify-between mb-6"> <div> <h2 className="text-xl font-bold">أهلاً، {user.name}</h2> <div className="text-sm text-gray-600">الرصيد: <span className="font-medium">{user.balance.toFixed(2)} ج.م</span></div> </div> <div className="flex items-center gap-2"> <button onClick={() => setScreen('dashboard')} className="px-3 py-2 rounded-lg bg-white shadow">لوحة</button> <button onClick={() => setScreen('history')} className="px-3 py-2 rounded-lg bg-white shadow">السجل</button> <button onClick={logout} className="px-3 py-2 rounded-lg bg-red-100 text-red-700">خروج</button> </div> </header>

<main className="max-w-3xl mx-auto">
    {screen === 'dashboard' && (
      <section className="bg-white p-6 rounded-2xl shadow mb-6">
        <h3 className="text-lg font-semibold mb-3">تعبئة رصيد</h3>
        <div className="flex gap-3 items-center">
          <input type="number" value={topupAmount} onChange={e => setTopupAmount(e.target.value)} placeholder="اكتب المبلغ" className="flex-1 p-3 border rounded-lg" />
          <button onClick={handleTopUp} className="px-4 py-2 rounded-lg bg-green-600 text-white">استمرار</button>
        </div>

        <div className="mt-6">
          <h4 className="font-medium mb-2">خدمات سريعة</h4>
          <div className="flex gap-3">
            <button className="px-3 py-2 rounded-lg bg-indigo-50">تعبئة سريعة 10</button>
            <button className="px-3 py-2 rounded-lg bg-indigo-50">تعبئة 20</button>
            <button className="px-3 py-2 rounded-lg bg-indigo-50">تعبئة 50</button>
          </div>
        </div>
      </section>
    )}

    {screen === 'history' && (
      <section className="bg-white p-6 rounded-2xl shadow">
        <h3 className="text-lg font-semibold mb-3">سجل المعاملات</h3>
        {transactions.length === 0 && <div className="text-gray-500">لا توجد معاملات بعد.</div>}
        <ul className="space-y-3">
          {transactions.map(tx => (
            <li key={tx.id} className="flex justify-between items-center p-3 border rounded-lg">
              <div>
                <div className="font-medium">{tx.type === 'topup' ? 'تعبئة' : 'تعبئة (تمويل)'}</div>
                <div className="text-sm text-gray-500">{tx.method} · {tx.date}</div>
              </div>
              <div className="font-semibold">{tx.amount.toFixed(2)} ج.م</div>
            </li>
          ))}
        </ul>
      </section>
    )}
  </main>

  {/* تمويل مودال */}
  {showFinanceModal && (
    <div className="fixed inset-0 bg-black/40 flex items-center justify-center p-4">
      <div className="bg-white w-full max-w-lg rounded-2xl p-6 shadow">
        <h3 className="text-lg font-semibold mb-3">اختر طريقة الدفع / التمويل</h3>
        <p className="text-sm text-gray-600 mb-4">المبلغ: <span className="font-medium">{parseFloat(topupAmount || 0).toFixed(2)} ج.م</span></p>
        <div className="grid grid-cols-2 gap-3 mb-4">
          <button onClick={() => confirmTopUp({ type: 'instant' })} className="p-3 rounded-lg border">دفع فوري (بطاقة)</button>
          <button onClick={() => confirmTopUp({ type: 'finance', period: 3 })} className="p-3 rounded-lg border">تمويل 3 أشهر</button>
          <button onClick={() => confirmTopUp({ type: 'finance', period: 6 })} className="p-3 rounded-lg border">تمويل 6 أشهر</button>
          <button onClick={() => confirmTopUp({ type: 'finance', period: 12 })} className="p-3 rounded-lg border">تمويل 12 شهر</button>
        </div>
        <div className="flex justify-end gap-3">
          <button onClick={() => setShowFinanceModal(false)} className="px-4 py-2 rounded-lg">إلغاء</button>
        </div>
      </div>
    </div>
  )}

  {loading && (
    <div className="fixed bottom-6 right-6 bg-white px-4 py-2 rounded-lg shadow">جاري المعالجة...</div>
  )}

  <footer className="max-w-3xl mx-auto text-center text-xs text-gray-400 mt-6">نموذج أولي - للاستخدام التجريبي فقط</footer>
</div>

); }

/* --- وثيقة المرفقات: API - قاعدة بيانات - تكاملات مقترحة --- ملخص سريع (استخدم هذه المواصفات لبناء الـ backend):

1. نموذج بيانات (قاعدة بيانات SQL أو NoSQL):



users: { id, name, email, phone, password_hash, balance, created_at }

transactions: { id, user_id, type, amount, method, metadata(json), status, created_at }

finance_loans: { id, user_id, amount, term_months, interest_rate, monthly_due, status, created_at }

audit_logs: { id, user_id, action, metadata, created_at }


2. واجهات API مقترحة (REST):



POST /api/auth/login  -> body: {phone/email, password} -> returns token, user

POST /api/topup -> auth header, body: {amount, method, finance_option?} -> creates transaction

GET /api/transactions -> auth -> returns user's transactions (pagination)

POST /api/finance/apply -> auth, body:{amount, term_months} -> creates loan request

GET /api/finance/{id} -> auth -> loan details


3. متطلبات الأمان:



توثيق JWT أو session مشفر

تخزين كلمات المرور باستخدام bcrypt/argon2

التحقق من المدفوعات عبر موفري دفع موثوقين (Stripe, Paymob, Fawry)

تدقيق عمليات الإيداع لمنع الغش


4. تكاملات الدفع المقترحة:



بطاقات الائتمان/خصم: Stripe أو Paymob (مصر)

المحافظ: PayPal, local wallets

الدفع النقدي عند الوكيل: تكامل مع فوري أو شبكة موزعين


5. قواعد العمل للتمويل:



تحقق من هوية المستخدم (KYC بسيط: رقم هاتف، بطاقة هوية عند الحاجة)

حاسبة فوائد بسيطة: interest_rate سنوي -> تحويل إلى دفعات شهرية

سياسة قبول القروض: مبلغ أقصى يعتمد على تاريخ المستخدم وترتيب الائتمان

واجهة لإدارة الدفعات المتأخرة وتنبيهات SMS/Email


6. ميزات مستقبلية (MVP -> v1 -> v2):



MVP: تسجيل، تعبئة رصيد، تمويل بسيط (خطط ثابتة)، سجل معاملات

v1: دمج مزود دفع، إشعارات، لوحة إدارة

v2: scoring ائتماني، دعم تعدد العملات، عروض ترويجية


--- نهاية المرفقات --- */

