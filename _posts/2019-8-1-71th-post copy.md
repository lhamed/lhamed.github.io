---
layout:
title:  iOS Entitlement Setting in Script. (Post Process )
description: 
modified: 2019-8-1
tags: [ Unity , GameDev, iOS , Xcode ] 
---

## 유니티 iOS 빌드 된 폴더를 Post Build Process 해서, Capability Entitlement 설정 하기 

오늘도 젠킨스로 iOS 빌드를 뽑아보는 데 , 클라우드 로드가 제대로 작동하지 않았다. 

지금 프로젝트는 Prime31 의 클라우드 에셋을 쓰기 때문에, 

( 그러고 보니 , 이 에셋을 쓰지 않고 구현하는 방법에 대해서 나중에 알아보자.)

Capbability 에서 Cloud 항목을 Enable 하고 , 세부 Entitlement 를 True 해주어야 하는데, 체크가 되어있었다.

(Cloud kit , Document , Key-value 등 )

사실 이 문제를 고친 해결책은 아니었지만, 그 과정에서 의심 가는 것들을 고치던 중에 위 내용을 알아냈다. 

```csharp
void SetEntitlementiOS()
{
    var file_name = "unity.entitlements";
    var proj_path = projectPath;
    var proj = new PBXProject();
    proj.ReadFromFile(proj_path);
    var target_name = PBXProject.GetUnityTargetName();
    var target_guid = proj.TargetGuidByName(target_name);
    var dst = pathToBuiltProject + "/" + target_name + "/" + file_name;
    try
    {
            File.WriteAllText(dst, entitlements);
            proj.AddFile(target_name + "/" + file_name, file_name);
            proj.AddBuildProperty(target_guid, "CODE_SIGN_ENTITLEMENTS", target_name + "/" + file_name);
            proj.WriteToFile(proj_path);
    }
    catch (IOException e)
    {
            Debug.Log("Could not copy entitlements. Probably already exists. " + e);
    }
}
    private const string entitlements = @"
     <?xml version=""1.0"" encoding=""UTF-8""?>
<!DOCTYPE plist PUBLIC ""-//Apple//DTD PLIST 1.0//EN"" ""http://www.apple.com/DTDs/PropertyList-1.0.dtd"">
<plist version=""1.0"">
<dict>
	<key>aps-environment</key>
	<string>production</string>
	<key>com.apple.developer.icloud-container-identifiers</key>
	<array>
		<string>iCloud.$(CFBundleIdentifier)</string>
	</array>
	<key>com.apple.developer.icloud-services</key>
	<array>
		<string>CloudKit</string>
		<string>CloudDocuments</string>
	</array>
	<key>com.apple.developer.ubiquity-container-identifiers</key>
	<array>
		<string>iCloud.$(CFBundleIdentifier)</string>
	</array>
	<key>com.apple.developer.ubiquity-kvstore-identifier</key>
	<string>$(TeamIdentifierPrefix)$(CFBundleIdentifier)</string>
</dict>
</plist>
";

```