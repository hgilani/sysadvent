# Effective System Administration

This was written by [Jennifer Davis](https://twitter.com/sigje).

For most of us, the end of year brings performance appraisals and reflection on
the year's setbacks and accomplishments both professional and personal. In the
glass bowl of life, I ask myself if I've made a difference, earned respect,
have I grown from where I started the year? Technology has brought us
innovation to hack our lives and measure our personal success through metrics.
For example measuring sleep, weight, and activity. For example, I can see how
much I slept, how fast I biked to work this morning, how often I biked, and the
steps forward (or back) towards my goals. There is a dearth in tools available
to measure personal work growth and effectiveness. 

Being an effective system administrator requires an ability to do several
(seemingly obvious but often rather fraught) things: To break down projects
into actions that we understand as a part, as a whole, and can manage in a
discrete period of time; explaining this roadmap to other teams; and
successfully keeping implementation on schedule while being flexible enough to
handle any issues that arise. The job descriptions and responsibilities of
system administrators can vary greatly in scope and the corresponding degrees
of difficulty and creativity necessary to succeed. Since "system administrator"
alone can sometimes function as a vague catch-all for such a diversity of tasks
and functions we use a variety of sometimes unwieldy names to better specify
our roles and focus. Regardless of title there is a great deal of commonality
in how teams we work for/with view us and depend upon our knowledge and skills.
In some cases it's a bit like being a member of a symphony in which the
strings, the brass, and the wind sections cannot agree upon the tempo or even
what piece to play.

At a team level, management has a vision of what the team should be doing and
how it should be working. Often our work is considered a cost center, something
that doesn't produce a direct profit and is generally first in line for cuts.
Management becomes focused on the bottom line to the detriment of building a
strong team and an encompassing vision. Teams are put in the unfortunate
position of competing for finite resources. For better or worse, the team that
"markets" itself best generally comes out ahead.

Rather than embracing the frustration that may come with a sub-optimal
allocation of time or resources, give your manager visuals to obtain the
resources you need by showing value and maintain focus on the team's vision.
Understand goals for the team, and know how your efforts fit into that vision.
By broadening your focus a little bit you may have more influence in
determining short term goals. Is there information that your manager is not
aware of that may change short term goals? Is he or she unaware of the
real-world time it takes to perform a particular task, or how project A by team
X will impact the ability of you and your team to complete project B?
Communicate information succinctly and clearly with your interpretation of the
data. Present not just the problems but potential solutions that can solve the
problem. Back your solutions with the metrics you collect about your own work. 

## Personal Metrics

The first part in creating visuals is to establish an efficient workflow that
you can measure. The metrics you collect over time will convince others of the
validity of your timetable and proposed project maps. To obtain metrics, break
big projects into tasks. Break large tasks into smaller tasks. A task should be
no more than 4 hours of work. The reality is that for most of us each 8 hour
work day allows for 4 hours of work.  The other 4 hours are taken up by
interrupt tasks, networking with individuals from other teams that your work
depends on, and communicating your status. Stop, take a deep breath, embrace
this reality, and then take the time to ensure that those 4 hours of work are
quality time. 

Qualify each task. This qualification is dependent on your environment. Sample
qualifications include prep, installation, deployment, monitoring, business
continuity, education, documentation and mentoring. Allocate the 4 hours of
interrupt tasks as a chunk of time labeled as "interrupt". Depending on your
work, your job may be 100% interrupt driven. If this is the kind of work you
enjoy doing then measuring your success will take more time. I measure my
interrupts by total time taken and scale of interrupts focusing my measurements
on non-interrupts. Ideally, my interrupt time is spent mostly on networking and
mentoring versus manual domain specific tasks that only I can do.

Make an informed estimate of how much time and effort each task will take.
Excessively rosy estimations can lead to unnecessary stress. Be conservative.
Everyone has peaks and valleys in terms of attention and performance that do
not always match up. For me, mornings are key to establish the work I'm going
to complete for the day with a couple of hours of concentrated work. Around
lunch time is my interrupt time and I try to schedule meetings then. I
re-evaluate my progress for the morning and finish up the day with
uninterrupted time.  Each task should be between 1-4 hours. Order your tasks
based on team goals and priorities. Sync up with your team and manager
regularly to ensure that you are working on the right projects and tasks. To
help keep my team in sync, I introduced a daily standup with the goal of 2
minutes max per person. Then in the weekly meeting with my manager, I asked
about team goals verifying that my prioritized list maps out to these goals. 

## Project and Large Task State

Determine the states of work your projects can have. Depending on the tools in
your environment the terms available may not map directly to your organization
of tasks. Your personal term association matters more than the actual terms. I
use "Accepted", "WIP", "Done", and "Validated". "Accepted" means I know about
it, and have accepted that I _own_ the responsibility of ensuring that the
work is done. I understand the specific goals and a finish state. "WIP" means
I've started progress on this task and it has status. It can involve further
clarification of goals, and some amount of progress. "Done" means that I
believe that the task has been completed. "Validated" means that I've verified
that the work has been completed either through buddy checks, management
acceptance, or some automated test to verify the completed state. In general I
try to find an external method to verify that the work is complete. 

Tracking the actual effort it takes to complete a task and the time each
project takes to pass through states that you have defined helps you measure
the time that it takes you to complete specific tasks and projects as well as
where the time is spent across the project between tasks. Measure your
completion of tasks and projects with your personal performance metrics. Think
about the questions that you'd like your manager to understand. These questions
should be specific to you, your work, and what value you bring to your job.
Examples include: How long does it take to complete a repetitive manual task?
How long would it take if you were given enough time to automate the manual
task? What would the effect of fixing a minor bug in the application have on
the overall time it takes for your team to complete manual task? Are you
getting better at completing tasks by doing more and finishing them faster?
Turn these metrics into graphs. Images convey meaning quickly. You can use R,
YUI Charts, Google Spreadsheets with charts to make some nifty graphs.   

Find or write tools that measure the completion of work. The data you collect
about your work provides information for your status reports, requests for out
of band raises, as well as end of year summary. Think through the tools and
processes in your environment. If you use bugzilla or RT for example find the
mechanisms that you can use to pull data straight from the source
automatically. If you manage the bugzilla database, you can pull this
information directly with mysql queries. If you don't investigate whether there
is an API provided that you can poll for this information.  Interesting metrics
include total tasks per day, average latency per task, average latency per type
of work, and percentage of time spent doing specific types of tasks. Note that
if you are spending less than 4 hours on interrupt tasks consistently, make
sure that you are spending adequate time reaching out to your peers in other
groups. Networking and understanding relevance is part of your job. 

Communicate the schedule and completion of tasks to everyone who is affected by
the completion and delays of your work. Consistent clear communication builds
your perceived value to management, team, and customers. Visuals give your
manager effective views of your value to use at performance review time to
ensure your salary increases.

## Learn to say no

When you organize your priorities and tasks towards improving your efficiency
and your manager's goals you have to learn to say no to some of the interrupts.
This is not the BOFH "no". This is an opportunity to increase your value. I
often struggle to say no when confronted with new and interesting problems or
when someone needs help with a problem that would be very easy for me to do.

When someone asks you for something, is it something that you _must_ do,
or can you teach them how to help themselves? Depending on the urgency invest
some time training the individual how to help themselves. Ideally you go to
their workspace and let them run through the process with your guidance while
keeping your hands off the keyboard. It's in the nature of a sysadmin to jump
in and help, so I hold my hands behind my back. This is also important during
emergencies to ensure that other's can be comfortable executing on common
problems. Tell them to take notes and document the procedure for your review
later. If the process is complicated you may need to run through this exercise
twice. By investing the time in training someone, you multiply the
effectiveness of getting this task done in the future. The next time someone
needs help you can point them to the documentation and if you are busy to the
person you previously trained. I have found that people get frustrated at first
through this process but over time that they appreciate that they can help
themselves and have more confidence in helping others through the same process.

If this is something you _must_ do, what is the impact of you stopping and
completing the request? Will the short term task unblock a big team objective?
How complicated is it and how much time will it take you to do it? When you
think of these questions this will give you the gut instinct of whether you
should go ahead and get the work done. Understand the work you are doing, and
_own_ your time. A good sys admin knows when she must fail to deliver on a
project due to unplanned interrupts with a higher priority. Management and key
stakeholders should be informed of compromised deadlines with brief details
about why the task was preempted. I find clear to the point communication
difficult so I solve this by creating a for more information link in the email
that points to a wiki. The wiki I can edit for clarity and more details as
needed. 

## Modify your behaviors

Over time you will see a trend in your behaviors. You can see what you like
about your job and whether you are spending time on the right kind of work. If
you do not like what you see in your status reports, change the way you work or
find a new job. At the end of the year you won't be feeling regret over missed
opportunities because you have a way to keep track of your value over time and
ensure that you are making progress. 

## Conclusion

Whatever kind of ops or administrator that your title or potential job
reflects, look at the opportunities you have to work more efficiently. The
effort you put into sending information out will decrease the number of times
you are pulled away from the task-in-progress to be solicited for information
piecemeal. Open up, network with others and you'll have more time to get deep
into the parts of your job that increase your satisfaction, effectiveness, and
bring your brain happiness. 

## Further Reading

* [Your own kind of moneyball: The Metrics that Measure You](http://blogs.hbr.org/johnson/2010/11/your-own-kind-of-moneyball-the.html)
* [Visibility and Communication](http://sysadvent.blogspot.com/2008/12/day-19-visibility-and-communication.html)
* [Time Management for System Administrators](http://www.amazon.com/Management-System-Administrators-Thomas-Limoncelli/dp/0596007833)
* [Don't be a human keyboard](http://sysadvent.blogspot.com/2010/12/day-13-dont-be-human-keyboard.html)
* [Share skills and permissions with code](http://sysadvent.blogspot.com/2011/12/day-3-share-skills-and-permissions-with.html)

