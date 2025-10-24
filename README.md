# UnitySciptableObjectEventSystem
A scriptable object based event system made for Unity 6.0 and below.

Custom Event System Setup Guide
Create a ScriptableObject Event
    Right-click in the Project Window → Create → GameEvent (name it after your event, e.g., OnPlayerDeath, OnScoreUpdated).

2. Attach the GameEventListener
    Add the GameEventListener component to any GameObject that should react to the event.

In the inspector:

Assign your GameEvent (e.g., drag OnScoreUpdated into the gameEvent field).

Click + in the response section to add a function call.

3. Trigger the Event from a Script
   In any script where you want to send the event:

csharp
public GameEvent OnScoreUpdated;  // Assign via inspector
Call it anywhere in your code:

4. Define the Response
   On the GameObject with the GameEventListener:

   In the response field, select a target object (e.g., a UI Text element).

   Choose a function (e.g., Text.SetText(string)) and map the event data.

   Example Workflow
   Scenario: Updating a score display when the player earns points.

   Create Event:

   Assets/Events/OnScoreUpdated.asset (a GameEvent ScriptableObject).

   Set Up Listener:

   Attach GameEventListener to your ScoreText GameObject.

   Assign OnScoreUpdated to the gameEvent field.

   Add a response:

   Target: ScoreText (Text component)

   Function: TextMeshProUGUI.SetText(string) (or UnityEngine.UI.Text.text)

   Argument: (int)data (assuming scoreValue is an integer).

   Trigger from Player Script:

   csharp
   public GameEvent OnScoreUpdated;
   private int _score;

   void AddScore(int points) 
   {
       _score += points;
       OnScoreUpdated.Raise(this, _score);  // Updates UI automatically!
   }
