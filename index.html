import React from "react";

/**
 * Big Dipper (북두칠성) – Interactive Portfolio Constellation
 * - 배경: 이미지 / 절차적 모드
 * - 노드: 7개 별(프로필, 2-2, 3-1, 3-2, 4-1, 4-2, 5-1)
 * - UI: 우측하단 호버 패널, 비율 선택(1/1, 16/9, 21/9, 3/1)
 * - 저장: 커스텀 배경 이미지를 localStorage에 저장/복원
 * - 테스트: 개발 모드에서 간단한 self-tests로 안정성 점검
 *
 * ⚙️ 최근 에러(React #130) 대응: children에 object를 직접 렌더링하지 않도록 문자열/ReactElement만 유지
 */

// 작품 정보 (좌→우)
const defaultWorks = [
  { id: 1, key: "Dubhe",  label: "프로필", desc: "소개 / 연락처 / 링크", href: "#profile" },
  { id: 2, key: "Merak",  label: "2-2",   desc: "프로젝트 2-2 개요", href: "#work-2-2" },
  { id: 3, key: "Phecda", label: "3-1",   desc: "프로젝트 3-1 기능", href: "#work-3-1" },
  { id: 4, key: "Megrez", label: "3-2",   desc: "프로젝트 3-2 인터랙션", href: "#work-3-2" },
  { id: 5, key: "Alioth", label: "4-1",   desc: "프로젝트 4-1 디자인 시스템", href: "#work-4-1" },
  { id: 6, key: "Mizar",  label: "4-2",   desc: "프로젝트 4-2 최적화", href: "#work-4-2" },
  { id: 7, key: "Alkaid", label: "5-1",   desc: "프로젝트 5-1 성과", href: "#work-5-1" },
];

// 북두칠성 베이스 좌표 (뷰박스 0~100)
const starLayout = [
  { id: 1, x: 10, y: 20 },
  { id: 2, x: 16, y: 50 },
  { id: 3, x: 36, y: 60 },
  { id: 4, x: 47, y: 40 },
  { id: 5, x: 62, y: 34 },
  { id: 6, x: 73, y: 30 },
  { id: 7, x: 86, y: 36 },
];

function mergeWorksWithLayout(works) {
  return starLayout.map((pos, i) => ({ ...pos, ...(works[i] || {}), index: i }));
}

export default function BigDipperPortfolio({
  works = defaultWorks,
  title = "B935016 고영광",
  backgroundMode = "image", // 'image' | 'procedural'
  backgroundImageUrl = "https://images.unsplash.com/photo-1523986371872-9d3ba2e2b1b9?q=80&w=1600&auto=format&fit=crop",
  showOverlayStars = false,
  canvasAspect = "16/9",
  dipperScaleX = 0.85,   // 가로 압축
  dipperScale = 0.8,     // 전체 크기 축소
  dipperRotateDeg = 205, // 현재 각도(시계방향)
  dipperPivotIndex = 4,  // 회전 피벗(1~7)
  dipperOffsetX = 0,
  dipperOffsetY = 0,
  dipperMirrorX = true,
}) {
  // --- state ---
  const [bgOk, setBgOk] = React.useState(true);
  const [customBgDataUrl, setCustomBgDataUrl] = React.useState("");
  const [active, setActive] = React.useState(null); // {label, desc, href}
  const [aspect, setAspect] = React.useState(canvasAspect);
  const fileInputRef = React.useRef(null);

  // 로컬 저장된 배경 복원
  React.useEffect(() => {
    try {
      const saved = typeof window !== 'undefined' ? window.localStorage.getItem('dipper:bg') : null;
      if (saved) setCustomBgDataUrl(saved);
    } catch (e) {
      console.error('[BigDipper] load bg failed', e);
    }
  }, []);

  const bgHref = customBgDataUrl && typeof customBgDataUrl === 'string' && customBgDataUrl.length > 0
    ? customBgDataUrl
    : backgroundImageUrl;

  // 제목
  React.useEffect(() => { if (typeof document !== 'undefined') document.title = title; }, [title]);

  // 비율 파싱
  const aspectScale = React.useMemo(() => {
    const m = String(aspect).split('/');
    const w = Math.max(1, parseFloat(m[0] || '16'));
    const h = Math.max(1, parseFloat(m[1] || '9'));
    return { w, h, k: w / h };
  }, [aspect]);

  // 좌표 파이프라인
  const nodesBase = React.useMemo(() => mergeWorksWithLayout(works), [works]);
  const nodesScaled = React.useMemo(
    () => nodesBase.map(n => ({ ...n, x: n.x * aspectScale.k })),
    [nodesBase, aspectScale.k]
  );
  const nodesAdjusted = React.useMemo(() => {
    const cx = (100 * aspectScale.k) / 2;
    const s = Math.max(0.5, Math.min(1, dipperScaleX));
    return nodesScaled.map(n => ({ ...n, x: cx + (n.x - cx) * s }));
  }, [nodesScaled, aspectScale.k, dipperScaleX]);
  const nodesSized = React.useMemo(() => {
    const cx = (100 * aspectScale.k) / 2;
    const cy = 50;
    const s = Math.max(0.6, Math.min(1.2, dipperScale));
    return nodesAdjusted.map(n => ({
      ...n,
      x: cx + (n.x - cx) * s,
      y: cy + (n.y - cy) * s,
    }));
  }, [nodesAdjusted, aspectScale.k, dipperScale]);
  const nodesFinal = React.useMemo(() => {
    // 피벗 회전
    const cx = (100 * aspectScale.k) / 2;
    const cy = 50;
    const pivotIdx = Math.max(1, Math.min(7, dipperPivotIndex)) - 1;
    const pivot = nodesSized[pivotIdx] || { x: cx, y: cy };
    const rad = (Math.PI / 180) * (dipperRotateDeg || 0);
    const cos = Math.cos(rad); const sin = Math.sin(rad);
    return nodesSized.map(n => {
      const dx = n.x - pivot.x, dy = n.y - pivot.y;
      return {
        ...n,
        x: pivot.x + dx * cos - dy * sin + dipperOffsetX,
        y: pivot.y + dx * sin + dy * cos + dipperOffsetY,
      };
    });
  }, [nodesSized, aspectScale.k, dipperRotateDeg, dipperOffsetX, dipperOffsetY, dipperPivotIndex]);
  const nodesScreen = React.useMemo(() => {
    if (!dipperMirrorX) return nodesFinal;
    const cx = (100 * aspectScale.k) / 2;
    return nodesFinal.map(n => ({ ...n, x: cx * 2 - n.x }));
  }, [nodesFinal, dipperMirrorX, aspectScale.k]);

  const polylinePoints = React.useMemo(
    () => nodesScreen.map(n => `${n.x},${n.y}`).join(' '),
    [nodesScreen]
  );

  // 연결선 스타일
  const LINK_STROKE_WIDTH = 0.35;
  const LINK_STROKE_OPACITY = 0.35;
  const LINK_HALO_WIDTH = 0.55;
  const LINK_HALO_OPACITY = 0.18;

  // 개발용 self-tests (간단)
  React.useEffect(() => {
    if (typeof process !== 'undefined' && process.env && process.env.NODE_ENV === 'production') return;
    try {
      const assert = (c, m) => { if (!c) throw new Error(m); };
      assert(Array.isArray(starLayout) && starLayout.length === 7, 'starLayout length');
      const merged = mergeWorksWithLayout(defaultWorks); assert(merged.length === 7, 'merge 7');
      assert(typeof polylinePoints === 'string' && polylinePoints.split(' ').length === 7, '7 points polyline');
      const vbw = 100 * aspectScale.k; assert(Number.isFinite(vbw), 'viewBox width finite');
      // 타입 안정성: children에 object가 직접 들어가지 않는지 간접 확인
      assert(typeof (defaultWorks[0].label) === 'string', 'label string');
      assert(typeof (defaultWorks[0].desc) === 'string', 'desc string');
      assert(typeof (defaultWorks[0].href) === 'string', 'href string');
      // 🔎 추가 테스트: 외부 링크 판별 로직 간단 검증
      const testExternal = (u) => /^https?:/i.test(String(u));
      assert(testExternal('https://ex.com') && !testExternal('/local') && !testExternal('#a'), 'isExternal regex');
      console.info('[BigDipper] self-tests passed');
    } catch (e) {
      console.warn('[BigDipper] self-tests failed:', e);
    }
  }, [polylinePoints, aspectScale.k]);

  return (
    <main className="relative min-h-screen w-full bg-black text-white overflow-hidden">
      {/* 배경 그라데이션 */}
      <div aria-hidden className="pointer-events-none absolute inset-0 opacity-80" style={{ background: 'radial-gradient(circle at 50% 50%, #000010 0%, #000000 80%)' }} />

      {/* 헤더 */}
      <header className="relative z-10 mx-auto max-w-5xl px-6 pt-10 pb-6 flex items-center justify-between">
        <h1 className="text-2xl md:text-3xl font-semibold tracking-tight">{title}</h1>
        <div className="flex items-center gap-2">
          <div className="hidden md:flex items-center gap-1 text-xs text-white/70 mr-2">
            <span>비율:</span>
            {['1/1','16/9','21/9','3/1'].map(opt => (
              <button key={opt} onClick={() => setAspect(opt)} className={`px-2 py-1 rounded-md border ${aspect===opt?'bg-white/20 border-white/30':'bg-white/5 border-white/10 hover:bg-white/10'}`}>{opt}</button>
            ))}
          </div>
          <p className="hidden md:block text-sm text-white/70">별을 클릭하면 작품으로 이동합니다 ✨</p>
          <button onClick={() => fileInputRef.current?.click()} className="text-xs md:text-sm px-3 py-1.5 rounded-xl bg-white/10 hover:bg-white/15 border border-white/15">배경 이미지 선택</button>
          <input ref={fileInputRef} type="file" accept="image/*" className="hidden" onChange={(e) => {
            const f = e.target.files?.[0]; if (!f) return;
            const reader = new FileReader();
            reader.onload = (ev) => {
              const dataUrl = String(ev.target?.result || '');
              setCustomBgDataUrl(dataUrl); setBgOk(true);
              try { window.localStorage.setItem('dipper:bg', dataUrl); } catch (err) { console.error('[BigDipper] save bg failed', err); }
            };
            reader.readAsDataURL(f);
          }} />
        </div>
      </header>

      {/* 안내/초기화 */}
      <div className="relative z-10 mx-auto max-w-5xl px-6 -mt-3 pb-2 flex gap-3 text-xs md:text-sm text-white/70">
        <button onClick={() => { try { window.localStorage.removeItem('dipper:bg'); setCustomBgDataUrl(''); setBgOk(true);} catch (e) { console.error('[BigDipper] clear bg failed', e);} }} className="px-3 py-1.5 rounded-xl bg-white/5 hover:bg-white/10 border border-white/15">기본 배경 초기화</button>
        <span className="opacity-70">선택한 배경은 브라우저에 저장되어 다음 방문에도 유지됩니다.</span>
      </div>

      {/* 캔버스 */}
      <section className="relative z-10 mx-auto max-w-5xl w-full px-4 pb-16">
        <div className="relative w-full rounded-2xl border border-white/10 shadow-2xl overflow-hidden" style={{ aspectRatio: aspect }}>
          <svg viewBox={`0 0 ${100 * aspectScale.k} 100`} preserveAspectRatio="xMidYMid meet" className="h-full w-full">
            <defs>
              <linearGradient id="blueCast" x1="0" y1="0" x2="0" y2="1">
                <stop offset="0%" stopColor="#0e1a3a" />
                <stop offset="100%" stopColor="#0a0f23" />
              </linearGradient>
              <filter id="glow" x="-50%" y="-50%" width="200%" height="200%">
                <feGaussianBlur stdDeviation="0.8" result="coloredBlur" />
                <feMerge>
                  <feMergeNode in="coloredBlur" />
                  <feMergeNode in="SourceGraphic" />
                </feMerge>
              </filter>
              <filter id="tinyGlow" x="-50%" y="-50%" width="200%" height="200%">
                <feGaussianBlur stdDeviation="0.25" result="b" />
                <feMerge>
                  <feMergeNode in="b" />
                  <feMergeNode in="SourceGraphic" />
                </feMerge>
              </filter>
            </defs>

            {/* 배경 */}
            {backgroundMode === 'image' && bgHref && bgOk ? (
              <image href={bgHref} x={0} y={0} width={100 * aspectScale.k} height={100} preserveAspectRatio="xMidYMid slice" crossOrigin="anonymous" onError={() => setBgOk(false)} />
            ) : (
              <rect x="0" y="0" width={100 * aspectScale.k} height="100" fill="#0b1024" />
            )}
            <rect x="0" y="0" width={100 * aspectScale.k} height="100" fill="url(#blueCast)" opacity="0.25" />

            {/* 절차적 배경 별 */}
            {backgroundMode !== 'image' && showOverlayStars && (
              Array.from({ length: 80 }).map((_, i) => {
                const seed = Math.sin((i + 1) * 9876.543) * 10000;
                const fx = seed - Math.floor(seed);
                const fy = Math.sin(seed * 1.7) - Math.floor(Math.sin(seed * 1.7));
                const x = Math.abs(fx) * 100; const y = Math.abs(fy) * 100;
                const r = 0.08 + ((i % 7) / 7) * 0.28; // 0.08~0.36
                const bluish = 205 + (i % 24); const alpha = 0.2 + ((i % 11) / 11) * 0.28;
                return (
                  <g key={i} transform={`translate(${x} ${y})`} opacity={0.9}>
                    <circle r={r + 0.08} fill="rgba(255,255,255,0.18)" filter="url(#tinyGlow)" />
                    <circle r={r} fill={`rgb(${bluish}, ${bluish + 18}, 255)`} opacity={alpha} />
                  </g>
                );
              })
            )}

            {/* 연결선 (헤일로 + 본선) */}
            <polyline points={polylinePoints} fill="none" stroke={`rgba(255,255,255,${LINK_HALO_OPACITY})`} strokeWidth={LINK_HALO_WIDTH} strokeLinejoin="round" strokeLinecap="round" vectorEffect="non-scaling-stroke" filter="url(#glow)" />
            <polyline points={polylinePoints} fill="none" stroke={`rgba(255,255,255,${LINK_STROKE_OPACITY})`} strokeWidth={LINK_STROKE_WIDTH} strokeLinejoin="round" strokeLinecap="round" vectorEffect="non-scaling-stroke" filter="url(#glow)" />

            {/* 별들 */}
            {nodesScreen.map((n, idx) => (
              <Node key={n.id ?? idx} data={n} onHover={setActive} />
            ))}
          </svg>

          {/* 정보 패널 */}
          <div className="pointer-events-none absolute right-3 bottom-3 md:right-4 md:bottom-4">
            <div className={`transition-all duration-200 backdrop-blur-md rounded-xl border border-white/15 shadow-lg ${active ? 'bg-black/35 opacity-100 translate-y-0' : 'bg-black/20 opacity-0 translate-y-2'} max-w-[70vw] md:max-w-sm`} style={{ pointerEvents: 'none' }}>
              <div className="px-4 py-3">
                <div className="text-xs uppercase tracking-wider text-white/60">Project</div>
                <div className="mt-0.5 text-base md:text-lg font-medium">{active?.label ?? '노드에 마우스를 올려보세요'}</div>
                <div className="mt-1 text-xs md:text-sm text-white/75 leading-snug line-clamp-3">{active?.desc ?? '우측하단에 프로젝트 이름과 설명이 표시됩니다.'}</div>
                {active?.href ? (
                  <div className="mt-2 text-xs text-white/70">링크: <span className="underline underline-offset-4">{active.href}</span></div>
                ) : null}
              </div>
            </div>
          </div>
        </div>
      </section>
    </main>
  );
}

function Node({ data, onHover }) {
  const { x, y, label, href } = data ?? {};
  const rOuter = 1.15;
  const rCore = 0.48;

  const isExternal = typeof href === 'string' && /^https?:/i.test(String(href));

  const handleEnter = () => onHover?.({ label: String(label || ''), desc: String(data?.desc || ''), href: String(href || '') });
  const handleLeave = () => onHover?.(null);

  return (
    <g transform={`translate(${x} ${y})`}>
      <a
        href={href}
        target={isExternal ? "_blank" : "_self"}
        rel={isExternal ? "noreferrer" : undefined}
        aria-label={`${label} 열기`}
        onMouseEnter={handleEnter}
        onMouseLeave={handleLeave}
        onFocus={handleEnter}
        onBlur={handleLeave}
      >
        <title>{label}</title>
        <circle r={4.8} fill="transparent" />
        <circle r={rOuter} fill="rgba(255,255,255,0.20)">
          <animate attributeName="r" values={`${rOuter};${rOuter + 0.8};${rOuter}`} dur="2.8s" repeatCount="indefinite" />
          <animate attributeName="opacity" values="0.20;0.12;0.20" dur="2.8s" repeatCount="indefinite" />
        </circle>
        <circle r={rCore} fill="#ffffff" filter="url(#glow)">
          <animate attributeName="r" values={`${rCore};${rCore + 0.3};${rCore}`} dur="1.8s" repeatCount="indefinite" />
        </circle>
      </a>
    </g>
  );
}
