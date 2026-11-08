# Tjipp

iPhone-app för registrering, inloggning och underskrift med användarens enhetsnyckel.
Kräver iOS 16 eller senare. Tjänsten är under utveckling och saknar Digg-godkännande.

## Bygg

Öppna `PassportCapture.xcodeproj` i Xcode och välj schemat `PassportCapture`.
CI använder Xcode 16.4. Beroenden är låsta i `Package.resolved`.

```sh
python3 scripts/project.py
xcodebuild -resolvePackageDependencies -project PassportCapture.xcodeproj -scheme PassportCapture -onlyUsePackageVersionsFromResolvedFile
xcodebuild -project PassportCapture.xcodeproj -scheme PassportCapture -configuration Release -destination 'generic/platform=iOS' CODE_SIGNING_ALLOWED=NO build
```

För installation på telefon: välj utvecklingsteam och bundle-ID, aktivera NFC Tag
Reading och App Attest och använd en serverkonfiguration som godtar appens team
och identifierare. Apples signering och distributionsvillkor gäller separat.
Ett eget bygge får inte automatiskt tillgång till Tjipps tjänst.

## Test

```sh
xcodebuild -project PassportCapture.xcodeproj -scheme PassportCapture -destination 'platform=iOS Simulator,name=iPhone 16 Pro' CODE_SIGNING_ALLOWED=NO test
```

Simulatorn provar vyer och protokollbindningar. NFC, Secure Enclave och App Attest
kräver fysisk telefon. Åldersbevisens nyckelkomponent ingår; fullständig utgivning
och presentation från appen återstår. Ett källbygge är inte en publicerad apputgåva.

## Integration och licens

För anslutande tjänster, se [Folk-idP](https://github.com/Jtensetti/Folk-idP).
Koden får byggas och användas oförändrad enligt [licensen](LICENSE).
Ändringar kräver tillstånd. Produktionsåtkomst, support och priser regleras separat.
[Tredjepartskomponenter](THIRD_PARTY.md) behåller sina egna licenser.
