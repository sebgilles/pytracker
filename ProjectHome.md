# Python APIs for Pivotal Tracker #

pytracker is a simple Python API that wraps the [Pivotal Tracker](http://www.pivotaltracker.com/) [REST APIs](https://www.pivotaltracker.com/help/api).

The API ships with an example that updates a Google Calendar with release dates.

## Examples ##

### Authenticate ###
```
from pytracker import Tracker
from pytracker import Story
from pytracker import HostedTrackerAuth

def main(argv):
  auth = HostedTrackerAuth('username', 'password')
  tracker = Tracker(10101, auth)
```

### Fetch a story ###
```
  story = tracker.GetStory(684566)
```

### Create a story ###
```
story = Story()
story.SetName('wake up')
story.SetEstimate(1)
tracker.AddNewStory(story)
```

### Update an existing story ###
```
story = tracker.GetStory(684566)
story.SetCurrentState('delivered')
tracker.UpdateStory(story)
```

### Add a comment ###
```
tracker.AddComment(story_id, 'The customer is always right.')
```

### Add a label ###
```
story = tracker.GetStory(44)
story.AddLabel("api")
tracker.UpdateStory(story)
```

### Query with filter ###
```
stories = tracker.GetStories('type:release')
```

See [Tracker Search Help](http://www.pivotaltracker.com/help#howcanasearchberefined) for query language.

### Apply an update to multiple stories ###
```
stories = tracker.GetStories('owner:"party cat"')
changes = Story()
changes.SetOwnedBy('bro')
changes.SetEstimate(8)
for story in stories:
  tracker.UpdateStoryById(story.GetStoryId(), changes)
```

### Delete a story ###
```
tracker.DeleteStory(44)
```