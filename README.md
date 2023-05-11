# 8.50-8.51-Offsets-Signatures

UWorld; 8.51 = 0x5B4BEC0
UWorld; 8.50 = 0x5B4C610
OwningGameInstance = 0x160;
LocalPlayers = 0x38;
PlayerController = 0x30;
PlayerCameraManager = 0x2D8;
AcknowledgedPawn = 0x2C0;
Levels = 0x138;
PersistentLevel = 0x30;
AActors = 0x98;
CustomTimeDilation = 0xC0;
ActorCount = 0xA0;
RootComponent = 0x158;
FireStartLoc = 0x708;
RelativeLocation = 0x144;
RelativeRotation = 0x150;
CurrentWeapon = 0x730;
PreviousWeapon = 0x6B0;
PlayerState = 0x260;
Mesh = 0x2A0;
SquadID = 0x799;
ProjectileGravityScale = 0x228;
bIsDying = 0x6D8;
bIsDBNO = 0x330;
WeaponData = 0x3E0;
DisplayName = 0x70;
PrimaryPickupItemEntry = 0x278;
ItemDefinition = 0x88;
Tier = 0x54;
LastFireTime = 0x6BC;
LastFireTimeVerified = 0x6C0;
ReloadTime = 0x468;
ReloadScale = 0x110; 
ChargeDownTime = 0x13C; 
bAlreadySearched = 0xBC9;
IsReloading = 0x271;

Project World to Screen
40 53 55 56 57 41 56 48 83 EC 30 33 FF 4D 8B F0
FName
40 53 55 56 57 41 56 48 81 EC 50 08 (With Encryption)
BoneMatrix (8.50 only) 8.51 bonematrix is different
E8 ? ? ? ? 83 38 FF 74 30 
FreeFN
48 89 5C 24 08 55 56 57 48 8B EC 48 83 EC 40 48 8B
LineOfSightTo
48 89 5C 24 18 56 57 41 56 48 83 EC 40 33 FF 48 8B F1 4D 8B F0 48 8B DA 48 8B CA 48 89 7C 24 68
GObjects
48 8B 05 ? ? ? ? 48 8B 0C C8 48 8B 04 D1 
ProcessEvent VTABLE
0x40 or 0x64 both works test yourself :)

camera works for both versions

struct CameraInfo
{
    Vector3 Location;
    Vector3 Rotation;
    float FieldOfView;
};
CameraInfo GetCameraInfo() {
    int64 ViewStates = ctx->read<int64>(fortnite->LocalPlayer + 0xC8);
    int64 ViewReference = ctx->read<int64>(ViewStates + 8);
    CameraInfo ret;
    ret.Location = ctx->read<Vector3>(ctx->read<__int64>(fortnite->UWorld + 0xF8));
    ret.Rotation.x = (asin(ctx->read<float>(ViewReference + 0x6e8)) * (180.0 / M_PI));
    ret.Rotation.y = ctx->read<float>(fortnite->RootComponent + 0x154);
    ret.FieldOfView = ctx->read<float>(fortnite->LocalPlayer + 0x41C);
    return ret;
}


everything else you are more then capable of getting if you see this page on github.

(all credits to bxtshit#3095 on discord)

 https://github.com/bxtshit
