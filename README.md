https://github.com/PierceLee0515/HW4/blob/main/b0a37c37-9a42-41be-ae73-801de6483600.mp4
<h1>HW4</h1>

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        VStack {
            Text("NBA analyze")
                .foregroundColor(.white)
                .font(.largeTitle)
                .fontWeight(.heavy)
                .foregroundStyle(.primary)
                .background(Image("Black"))
            TabView{
                Group{
                    WelcomeView()
                        .tabItem{
                            Image(systemName: "person.crop.circle")
                            Text("Welcome")
                        }
                    PositionView()
                        .tabItem {
                            Image(systemName: "list.dash")
                            Text("Categories")
                        }
                    PlayerView()
                        .tabItem {
                            Image(systemName: "link")
                            Text("items")
                        }
                }
                .toolbarBackground(Color.black, for: .tabBar)
                .toolbarBackground(.visible, for: .tabBar)
                .toolbarColorScheme(.dark, for: .tabBar)
            }
            .tint(.yellow)
        }
    }
}                           



import SwiftUI

struct TermAndDescription: Identifiable{
    var id = UUID()
    var term:String
    var image:String
    var description:String
}
var myDictionary = [
    TermAndDescription(term: "Kobe Bryent", image: "Kobe",description: "黑曼巴"),
    TermAndDescription(term: "Stephen Curry", image: "Cu",description: "射手"),
    TermAndDescription(term: "Kevin Durant", image: "Kd",description: "進攻機器"),
    TermAndDescription(term: "Kevin Garnett", image: "Kg",description: "the big ticket")
    ,
    TermAndDescription(term: "Lebron James", image: "Lbj",description: "小皇帝")
    ,
    TermAndDescription(term: "Allen Iverson", image: "Ali",description: "花式籃球")
    ,
    TermAndDescription(term: "Dirk Nowitzki", image: "Di",description: "金雞獨立")
    ,
    TermAndDescription(term: "Tim Duncan", image: "Tim",description: "石佛")
]



struct PlayerView: View{
    @State var currentCard = 0
    var body: some View{
        VStack{
            VStack{
                Text(myDictionary[currentCard].term)
                    .font(.title)
                    .padding(.all, 10)
                Image((myDictionary[currentCard].image))
                    .resizable()
                    .aspectRatio(contentMode: .fill)
                    .frame(width:300,height:300)
                    .cornerRadius(15)
                    .overlay{
                        RoundedRectangle(cornerRadius: 20)
                            .stroke(Color.brown, lineWidth: 4)
                    }
                Text(myDictionary[currentCard].description)
                    .font(.body)
                    .foregroundColor(.gray)
                    .padding(.all, 10)
            }
            .onTapGesture{
                if currentCard<myDictionary.count-1{
                    currentCard+=1
                }else{
                    currentCard=0
                }
            }
            Text("點擊查看下一張")
                .padding(.all, 10)
        }
    }
}


import SwiftUI
struct Category : Identifiable {
    var id = UUID()
    var name : String 
    var image : String 
    var description : String
} 
var categories = [
    Category(name: "Point guard", image: "Magic", description: "控球後衛的神"),
    Category(name: "Shooting guard", image: "MJ", description: "神"),
    Category(name: "Small forward", image: "Bird", description: "小前鋒的神"),
    Category(name: "Power forward", image: "Ho", description: "大前鋒的神"),
    Category(name: "Center", image: "O’Neal", description: "中鋒的神")
]

struct BasicImageRow : View {
    var thisCategory : Category
    var body: some View {
        HStack {
            Image(thisCategory.image)
                .resizable()
                .frame(width: 40, height: 40)
                .cornerRadius(5)
            Text(thisCategory.name)
        }
    }
}

struct CategoryDetailView : View {
    @Environment(\.presentationMode) var presentationMode 
    var thisCategory :Category
    var body: some View{
        ScrollView{
            VStack{
                Image(thisCategory.image)
                    .resizable()
                    .aspectRatio(contentMode: .fill)
                    .clipped()
                Text(thisCategory.name)
                    .font(.system(.title, design:.rounded))
                    .fontWeight(.black)
                Spacer()
                Text(thisCategory.description)
                    .font(.system(.subheadline, design:.rounded))
                    .fontWeight(.light)
                Spacer()
            }
        }
        .overlay(
            HStack{
                Spacer()
                VStack{
                    Button(action:{
                        self.presentationMode.wrappedValue.dismiss()
                    },label:{
                        Image(systemName:"chevron.down.circle.fill")
                            .font(.largeTitle)
                            .foregroundColor(.white)
                    })
                    .padding(.trailing, 20)
                    .padding(.top, 40)
                    Spacer()
                }
            }
        )
    }
}

struct PositionView : View {
    @State var showDetailView = false
    @State var selectedCategory: Category?
    var body: some View{
        NavigationView{
            List(categories){
                categoryItem in BasicImageRow(thisCategory:categoryItem)
                    .onTapGesture{
                        self.showDetailView = true
                        self.selectedCategory = categoryItem
                    }
            }
            .sheet(item: self.$selectedCategory){ thisCategory in CategoryDetailView(thisCategory: thisCategory)
            }
            .navigationBarTitle("分類項目")
        }
    }
}

import SwiftUI

struct WelcomeView: View {
    var body: some View {
        ZStack {
            Image("NBA")
                .resizable()
                .aspectRatio(contentMode: .fill)
            
        }
    }
}





```

