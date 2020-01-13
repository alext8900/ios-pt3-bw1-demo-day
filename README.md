# iOS PT 3 Demo Day

## Requirements

1. Fork and clone the repository
2. Create a pull request (PR) and tag your TL and instructor

**Add your:**

1. Slide deck (4 required slides in Keynote)
2. Add your links
3. Answer all the questions (Replace placeholders with your answers)
4. Video demo (2 minutes max), share YouTube video link

The video demo is for sharing your work on your portfolio, but it is also a fallback if you have a technical issue during demo time.

## Links (Add your links)

* Code:                         https://github.com/FoodieFun-BuildWeek/iOS* Trello/Github Project Kanban: https://trello.com/b/K0WZFKFB/build-week* 

Test Flight: https://testflight.apple.com/v1/invite/f2515ad6ab00438ba5595aa7f885ec111903da3c038a404ab53a783c7183000b5905b11c?ct=VXUQXR6S56&advp=10000&platform=ios

YouTube demo video: https://youtu.be/mCb5uG8t0YY
## Questions (Answer indented below)

1. What was your favorite feature to implement? Why?

   Maybe the delete feature, i had never done a delete network request and i was happy that it worked on my first try

2. What was your #1 obstacle or bug that you fixed? How did you fix it?

   Information not making its way to the detail view, i fixed it because in my prepare for segue function i called the wrong view controller
  
3. Share a chunk of code (or file) you're proud of and explain why.

    func deleteRestaurant(with id: Int, completion: @escaping (Result<Restaurant, NetworkError>) -> Void)
       {
           
           let requestURL = baseURL.appendingPathComponent("/restaurants/\(id)")
           
           var request = URLRequest(url: requestURL)
           
           guard let userId = loginController.token?.id else { return }
           let stringUserId = String(userId)
           
           request.httpMethod = HTTPMethod.delete.rawValue
           request.setValue("application", forHTTPHeaderField: "Content-Type")
           request.setValue(loginController.token?.token, forHTTPHeaderField: "Authorization")
           request.setValue(stringUserId, forHTTPHeaderField: "user_id")
           
           URLSession.shared.dataTask(with: request) { data, response, error in
               if let response = response as? HTTPURLResponse,
                   response.statusCode != 204 {
                   completion(.failure(.badAuth))
               }
               
               if let _ = error {
                   completion(.failure(.otherError))
               }
               
               guard let data = data else {
                   completion(.failure(.badData))
                   return
               }
               
               let decoder = JSONDecoder()

               do {
                   let restaurant = try decoder.decode(Restaurant.self, from: data)
                   completion(.success(restaurant))
               } catch {
                   print("Error decoding restaurant after deleting: \(error)")
                   completion(.failure(.noDecode))
               }
           }.resume()
       }
   }

why because it was the first time i did a delete network request with a backend server and it actually worked

4. What is your elevator pitch? (30 second description your Grandma or a 5-year old would understand)

Its a food journal where you can keep up with your restaurant visits and why you liked or why you hated it.
  
5. What is your #1 feature?

   i suppose being able to edit restaurants
  
6. What are you future goals?

   Add a nearby restaurants view controller

## Required Slides (Add your Keynote to your PR)

1. App Name / Team Slide
2. Elevator Pitch
3. Your #1 Feature (Customer facing — what can I do with your app?)
4. Future Goals

## Slide Requirements

1. 50 pt font minimum
2. Be concise — don't write sentences/paragraphs (put these in your slide notes for speaking)
3. 3-6 bullets maximum per slide
4. Do the squint test (can you read the text if you squint, if so, make the font bigger)
6. Images are always welcome
7. Do the Grandma Test (Would your Grandma understand you?)

### Optional Slides

1. Blooper: What's a funny bug or blooper? (screenshots/GIFs please)
2. Revenue Model: If the app was your sole source of income, how would you monetize it?

## Presentation Format

**7 minutes/team**

* 4 minute presentation (5 minute hard cap)
* 3 minutes of questions

We have ~12 teams presenting today — please practice your presentation with a timer (as a team), and make sure you fit within the time limit.

Plan on having one person present the slides and live demo. Please practice your presentation in front of a mirror or with your team 2-5 times. Have the app running and visible in QuickTime so you can quickly transition between slides and live demo.

* App Name / Team Slide (30 seconds)
* Elevator Pitch Slide (30 seconds)
* Your #1 Feature (30 seconds)
* Live Demo (2 minutes)
* Future Goals (30 seconds)
* Questions (3 minutes)

## Final Schedule

### 5th Day

* **Deadline**: 6pm Pacific Code Freeze: Submit your final PR
	* Required: Submit your final TestFlight MVP
* 6pm - 9pm Demo Day Prep and Help (or whenever your usual 5th day hours are)

### Monday

* **Deadline**: 5pm Pacific Submit your Slides (iOS Demo Day PR)
* Required: **iOS Demo Day @ 7pm Pacific** (You must present to complete build week)

