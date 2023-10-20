---
title:  "Set Tracker"
layout: post
categories: media
---


WWDC 2023 came with a ton of interesting new functionality that I had been hoping for and I created this application to explore. Specifically, SwiftData and Swift Charts were extremely interesting. I had familiar working with the Core Data  APIs in previous applications, but found it a less than ideal integration into MVVM and SwiftUI.

The application that I would explore these new features with is design to keep track of setting at a rock gym. So what dose it do? Saves all of the logistical information you need to track for commercial gym setting (SwiftData), and cleanly presents the data in a visual manner that is easily digestible (Swift Charts).

Swift data is amazing, and was simultaneously the easiest and hardest part of developing this application. On the easy side, creating your models is trivial: 
```Swift
@Model
final class Gym {
    let id: UUID
    var name: String
    @Relationship(deleteRule: .cascade) var zones: [Zone]
    var difficultyCurve: DifficultyCurve
    
    var climbs: [Climb] {
        get {
            zones.flatMap { $0.climbs }
        }
    }
    
    init(name: String, zones: [Zone], difficultyCurve: DifficultyCurve = DifficultyCurve()) {
        self.id = UUID()
        self.name = name
        self.zones = zones
        self.difficultyCurve = difficultyCurve
    }
}
```

You can see above I just created my top level object by simply marked it as ``@model final class`` and **boom** all the work is done, it's now capable of being saved. You can see I'm even managing my relationships to other saved objects with the ``@Relationship`` macro.

On the hard side is the fact that it was a beta. This is my first true, deep dive, into a beta software release for Xcode, and the number of times functionality changed out from underneath me and broke my application was very annoying. However I learned a lot watching Apple and the community puzzling out the best way to handle certain features.
