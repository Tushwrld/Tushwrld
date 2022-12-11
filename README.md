- 👋 Hi, I’m @Tushwrld
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Tushwrld/Tushwrld is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
SHARE
Share with Flare
Docs

STACK

CONTEXT

DEBUG
CREATE SHARE
DOCS

Ignition Settings
Docs
EDITOR

PhpStorm
THEME
Auto
SAVE SETTINGS
Settings will be saved locally in ~/.ignition.json.

Attempt to read property "type" on null
ErrorException
PHP 8.1.9
9.28.0
Attempt to read property "type" on null

Expand vendor frames
Illuminate
 \ 
Foundation
 \ 
Bootstrap
 \ 
HandleExceptions
 
: 178
handleError
1 vendor frame
App
 \ 
Http
 \ 
Controllers
 \ 
Admin
 \ 
AmbassadorController
 
: 178
getReferral
43 vendor frames
public
 / 
index
.php
 
: 52
[top]
app
 / 
Http
 / 
Controllers
 / 
Admin
 / 
AmbassadorController
.php
 
: 178































            $users = $users->paginate(10);

            $users->appends(['q' => $search]);

        } else {

            $users = DB::table('events_users')

                ->select(

                    'users.name as firstname',

                    'users.lastname',

                    'events.name as event_name',

                    'events.point',

                    'users.created_at',

                    'events_users.status',

                    'users.email',

                    'users.type'

                )

                ->join('users', 'users.id', '=', 'events_users.user_id')

                ->join('events', 'events_users.event_id', '=', 'events.code');



            if (Auth::user()->type === 2 || Auth::user()->type === 3) {

                $users = $users->where('users.referrer_id', '=',  Auth::id());

            } else {

                $users = $users->where('events_users.created_at', '>=', $this->dateStart);

            }



            $users = $users->paginate(10);

        }



        return view('referral')->with('data', $users);

    }
