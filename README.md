# 📱 Synergym Android WebView

> Mobile App for AI-Powered Fitness Platform

Synergym의 Android 모바일 애플리케이션입니다. WebView를 기반으로 구축되어 웹 프론트엔드와 네이티브 Android 기능을 연결하는 하이브리드 앱입니다.

## 🚀 빠른 시작

### 필수 요구사항
- Android Studio Arctic Fox (2020.3.1) 이상
- Android SDK API Level 24+ (Android 7.0)
- Kotlin 2.0.21+
- Gradle 8.11.1+

### 프로젝트 설정

```bash
# 프로젝트 클론
git clone <repository-url>
cd webview

# Android Studio에서 프로젝트 열기
# File > Open > webview 폴더 선택

# 의존성 동기화
./gradlew sync

# 앱 빌드
./gradlew assembleDebug

# 디바이스/에뮬레이터에 설치
./gradlew installDebug
```

## 🛠️ 기술 스택

### 핵심 프레임워크
- **Android SDK API 36** (Android 14)
- **Kotlin 2.0.21** - 메인 개발 언어
- **Android Gradle Plugin 8.11.1** - 빌드 시스템

### Android 라이브러리
- **AndroidX Core KTX** - Kotlin 확장 함수
- **AppCompat** - 하위 호환성
- **Material Design Components** - Google Material UI

### WebView 기능
- **WebView** - 웹 콘텐츠 렌더링
- **WebChromeClient** - JavaScript 지원
- **WebViewClient** - 네비게이션 제어

### 개발 도구
- **JUnit 4** - 단위 테스트
- **Espresso** - UI 테스트
- **ProGuard** - 코드 난독화 (릴리즈)

## 📁 프로젝트 구조

```
webview/
├── app/
│   ├── build.gradle.kts           # 앱 모듈 빌드 설정
│   ├── proguard-rules.pro         # ProGuard 설정
│   └── src/
│       ├── main/
│       │   ├── AndroidManifest.xml     # 앱 매니페스트
│       │   ├── java/com/synergym/webview/  # 메인 소스 코드
│       │   │   ├── MainActivity.kt          # 메인 액티비티
│       │   │   ├── WebViewActivity.kt       # WebView 액티비티
│       │   │   ├── SplashActivity.kt        # 스플래시 화면
│       │   │   ├── utils/                   # 유틸리티 클래스
│       │   │   └── services/                # 네이티브 서비스
│       │   └── res/                    # 리소스 파일
│       │       ├── layout/             # 레이아웃 XML
│       │       ├── values/             # 문자열, 색상, 스타일
│       │       ├── drawable/           # 이미지 리소스
│       │       └── mipmap/             # 앱 아이콘
│       ├── test/                       # 단위 테스트
│       └── androidTest/                # 계측 테스트
├── build.gradle.kts                    # 프로젝트 빌드 설정
├── gradle.properties                   # Gradle 속성
├── settings.gradle.kts                 # 프로젝트 설정
└── gradle/
    └── libs.versions.toml              # 버전 카탈로그
```

## 🎯 주요 기능

### 📱 WebView 통합
- **하이브리드 앱**: 웹 콘텐츠를 네이티브 앱에서 실행
- **JavaScript Bridge**: 웹-네이티브 간 양방향 통신
- **자동 업데이트**: 웹 업데이트 시 앱 스토어 업데이트 불필요

### 🔧 네이티브 기능
- **카메라 액세스**: 운동 사진/영상 촬영
- **파일 업로드**: 갤러리에서 이미지 선택
- **알림 (Push Notification)**: 운동 리마인더
- **GPS 위치**: 야외 운동 추적
- **디바이스 센서**: 가속도계, 자이로스코프

### 🌐 웹 연동
- **자동 로그인**: 토큰 기반 세션 관리
- **오프라인 지원**: 캐시된 콘텐츠 표시
- **딥링크**: 특정 페이지로 직접 이동

## ⚙️ 앱 설정

### build.gradle.kts (앱 모듈)
```kotlin
android {
    namespace = "com.synergym.webview"
    compileSdk = 36

    defaultConfig {
        applicationId = "com.synergym.webview"
        minSdk = 24        // Android 7.0+
        targetSdk = 36     // Android 14
        versionCode = 1
        versionName = "1.0"
    }

    buildTypes {
        release {
            isMinifyEnabled = true
            proguardFiles(
                getDefaultProguardFile("proguard-android-optimize.txt"),
                "proguard-rules.pro"
            )
        }
    }

    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_11
        targetCompatibility = JavaVersion.VERSION_11
    }

    kotlinOptions {
        jvmTarget = "11"
    }
}
```

### AndroidManifest.xml 권한
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
```

## 🎨 UI/UX 디자인

### Material Design
- **Material 3** 디자인 시스템 적용
- **다크/라이트 테마** 지원
- **반응형 레이아웃** (폰/태블릿)

### 스플래시 화면
- **앱 로딩** 시 Synergym 브랜딩 표시
- **WebView 초기화** 동안 로딩 인디케이터

### 네비게이션
- **하단 네비게이션**: 주요 섹션 빠른 이동
- **백 버튼**: 웹 히스토리 네비게이션
- **풀스크린**: 몰입형 운동 경험

## 🔧 WebView 설정

### JavaScript 인터페이스
```kotlin
class WebAppInterface(private val context: Context) {
    @JavascriptInterface
    fun openCamera() {
        // 카메라 열기
    }
    
    @JavascriptInterface
    fun uploadFile() {
        // 파일 업로드
    }
    
    @JavascriptInterface
    fun sendNotification(message: String) {
        // 푸시 알림 전송
    }
}
```

### WebView 최적화
```kotlin
webView.settings.apply {
    javaScriptEnabled = true
    domStorageEnabled = true
    allowFileAccess = true
    allowContentAccess = true
    setGeolocationEnabled(true)
    mediaPlaybackRequiresUserGesture = false
}
```

## 📱 지원 디바이스

### 최소 요구사항
- **Android 7.0** (API Level 24) 이상
- **RAM**: 2GB 이상
- **저장공간**: 100MB 이상

### 권장 사양
- **Android 10.0** (API Level 29) 이상
- **RAM**: 4GB 이상
- **카메라**: 후면 카메라 (운동 분석용)

### 화면 크기
- **폰**: 4.0" ~ 7.0"
- **태블릿**: 7.0" ~ 12.0"
- **폴더블**: Galaxy Fold, Pixel Fold 지원

## 🧪 테스트

### 단위 테스트
```bash
./gradlew test
```

### UI 테스트 (Espresso)
```bash
./gradlew connectedAndroidTest
```

### 성능 테스트
```bash
./gradlew :app:connectedCheck
```

## 🚀 빌드 & 배포

### 디버그 빌드
```bash
./gradlew assembleDebug
```

### 릴리즈 빌드
```bash
# 키스토어 설정 후
./gradlew assembleRelease
```

### Google Play Store 배포
```bash
# AAB (Android App Bundle) 생성
./gradlew bundleRelease
```

### 빌드 변형 (Build Variants)
- **debug**: 개발 및 테스트용
- **release**: 프로덕션 배포용
- **staging**: 스테이징 환경 테스트용

## 🔐 보안 설정

### 네트워크 보안
```xml
<!-- res/xml/network_security_config.xml -->
<network-security-config>
    <domain-config cleartextTrafficPermitted="false">
        <domain includeSubdomains="true">synergym.app</domain>
    </domain-config>
</network-security-config>
```

### SSL 인증서 고정
```kotlin
// Certificate pinning 구현
```

### 데이터 보호
- **앱 데이터 암호화**
- **키체인 보안 저장소**
- **루팅 탐지**

## 📊 성능 최적화

### WebView 최적화
- **캐시 관리**: 이미지 및 리소스 캐싱
- **메모리 관리**: WebView 메모리 해제
- **네트워크 최적화**: Gzip 압축 지원

### 앱 크기 최적화
- **ProGuard**: 코드 난독화 및 최적화
- **R8**: 코드 축소
- **벡터 드로어블**: PNG 대신 SVG 사용

## 📱 플랫폼별 기능

### Android 전용 기능
- **적응형 아이콘**: Android 8.0+
- **알림 채널**: Android 8.0+
- **스코프드 스토리지**: Android 10+
- **다크 테마**: Android 10+

### 접근성 (Accessibility)
- **TalkBack** 지원
- **큰 텍스트** 지원
- **고대비 모드** 지원

## 🤝 기여하기

1. 브랜치 생성: `git checkout -b feature/안드로이드-새기능`
2. 코드 작성 및 테스트
3. 린팅: `./gradlew ktlintCheck`
4. 테스트: `./gradlew test connectedAndroidTest`
5. 커밋: `git commit -m "feat: 새로운 네이티브 기능 추가"`
6. Pull Request 생성

### 코딩 컨벤션
- **Kotlin 스타일 가이드** 준수
- **ktlint** 린터 사용
- **Detekt** 정적 분석

## 📝 라이선스

MIT License

---

📱 **Powered by Android + Kotlin + WebView**
