[README_ShopEase.md](https://github.com/user-attachments/files/28584219/README_ShopEase.md)
# 🛍️ ShopEase — Flutter E-Commerce App

<p align="center">
  <img src="https://img.shields.io/badge/Flutter-3.41.6-02569B?style=for-the-badge&logo=flutter&logoColor=white"/>
  <img src="https://img.shields.io/badge/Dart-3.11.4-0175C2?style=for-the-badge&logo=dart&logoColor=white"/>
  <img src="https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black"/>
  <img src="https://img.shields.io/badge/Platform-Android%20%7C%20iOS-green?style=for-the-badge"/>
</p>

> A modern, full-featured e-commerce mobile application built with Flutter and Firebase — featuring secure authentication, real-time product listings, profile photo upload, and a smooth shopping experience.

---

## ✨ Features

- 🔐 **Secure Authentication** — Firebase Auth with email/password login, registration & session persistence
- 🛒 **Product Catalog** — Real-time product listings fetched from Cloud Firestore
- 📸 **Profile Photo Upload** — Pick and upload user avatars to Firebase Storage via image_picker
- 🔗 **Share Products** — Native share sheet integration using share_plus
- ✨ **Shimmer Loading** — Skeleton placeholders during data fetch for polished UX
- 🌐 **REST API Integration** — HTTP client for external product/data endpoints
- 📱 **Responsive UI** — Clean Material Design 3 layouts across all screen sizes
- 🕐 **Date Formatting** — Localized date/time display using the intl package

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | Flutter 3.41.6 |
| Language | Dart 3.11.4 |
| Auth | Firebase Authentication |
| Database | Cloud Firestore |
| File Storage | Firebase Storage |
| Image Handling | image_picker |
| Sharing | share_plus |
| UI Enhancement | Shimmer, Material Design 3 |
| Networking | http ^1.1.0 |
| Localization | intl ^0.19.0 |

---

## 📁 Project Structure

```
lib/
├── main.dart                  # App entry point & Firebase init
├── firebase_options.dart      # Firebase platform config (multi-platform)
├── models/
│   ├── product_model.dart     # Product data model
│   └── user_model.dart        # User profile model
├── services/
│   ├── auth_service.dart      # Firebase Auth wrapper
│   ├── firestore_service.dart # Firestore CRUD operations
│   └── storage_service.dart   # Firebase Storage upload handler
├── screens/
│   ├── splash_screen.dart     # Splash with auth state check
│   ├── auth/
│   │   ├── login_screen.dart
│   │   └── register_screen.dart
│   ├── home/
│   │   └── home_screen.dart   # Product listing with shimmer
│   ├── product/
│   │   └── product_detail.dart
│   └── profile/
│       └── profile_screen.dart  # Avatar upload + share
└── widgets/
    ├── product_card.dart      # Reusable product card
    └── shimmer_card.dart      # Loading placeholder
```

---

## 🚀 Getting Started

### Prerequisites

- Flutter SDK `>=3.3.0 <4.0.0`
- Dart SDK `^3.11.0`
- Android Studio / VS Code
- Firebase project with Android & iOS configured

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/mihir-patel819/shopease-flutter.git
cd shopease-flutter

# 2. Install dependencies
flutter pub get

# 3. Add your Firebase config files
#    - android/app/google-services.json
#    - ios/Runner/GoogleService-Info.plist
#    - lib/firebase_options.dart  (run: flutterfire configure)

# 4. Run the app
flutter run
```

### Firebase Setup

1. Go to [Firebase Console](https://console.firebase.google.com/) and create a project
2. Enable **Email/Password** authentication
3. Create a **Cloud Firestore** database with this structure:
   ```
   products/
     {productId}/
       name: string
       price: number
       imageUrl: string
       description: string
       category: string
   users/
     {uid}/
       name: string
       email: string
       photoUrl: string
       createdAt: timestamp
   ```
4. Enable **Firebase Storage** and set rules for authenticated uploads
5. Run `flutterfire configure` to generate `firebase_options.dart`

---

## 📦 Dependencies

```yaml
firebase_core: ^3.10.1
firebase_auth: ^5.4.1
cloud_firestore: ^5.6.2
firebase_storage: ^12.4.10
image_picker: ^1.0.7
http: ^1.1.0
shimmer: ^3.0.0
intl: ^0.19.0
share_plus: ^10.1.4
```

---

## 🔥 Key Implementation Highlights

**Firebase Storage — Profile Photo Upload**
```dart
Future<String> uploadProfilePhoto(File imageFile, String uid) async {
  final ref = FirebaseStorage.instance.ref().child('profiles/$uid.jpg');
  final uploadTask = await ref.putFile(imageFile);
  return await uploadTask.ref.getDownloadURL();
}
```

**Firestore Real-time Product Stream**
```dart
Stream<List<Product>> getProducts() {
  return FirebaseFirestore.instance
      .collection('products')
      .snapshots()
      .map((snap) => snap.docs.map((d) => Product.fromMap(d.data())).toList());
}
```

**Shimmer Loading Placeholder**
```dart
Shimmer.fromColors(
  baseColor: Colors.grey[300]!,
  highlightColor: Colors.grey[100]!,
  child: ProductCardSkeleton(),
)
```

---

## 🔒 Firebase Security Rules (Firestore)

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /products/{productId} {
      allow read: if request.auth != null;
    }
    match /users/{uid} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```

---

## 🤝 Contributing

1. Fork the repo
2. Create your feature branch: `git checkout -b feature/NewFeature`
3. Commit your changes: `git commit -m 'Add NewFeature'`
4. Push to the branch: `git push origin feature/NewFeature`
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Mihir Patel**
- GitHub: [@mihir-patel819](https://github.com/mihir-patel819)
- LinkedIn: [linkedin.com/in/mihir-patel819](https://linkedin.com/in/mihir-patel819)
- Email: mihir5827@gmail.com

---

<p align="center">⭐ Star this repo if you found it helpful!</p>
