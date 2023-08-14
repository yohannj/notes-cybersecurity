# What is it
Shell allowing .NET commands (cmdlets). They return objects.

Cmdlets are represented as "Verb-Noun"

# Getting help
```powershell
Get-Help # Get-Help Get-Command -examples
```

# Example of commands
```powershell
Get-Help # Get-Help Get-Command -examples

# Find equivalent to linux
Get-Alias

# List available commands
Get-Command Verb-*
Get-Command *-Noun

# Chaining commands
Get-Command | Get-Member -MemberType Method

# Filtering
# operator: EQ, NE, NOT, GE, GT, Contains, ... => https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/where-object?view=powershell-7.2&viewFallbackFrom=powershell-6
Verb-Noun | Where-Object -Property PropertyName -operator Value 

# Search file on disk
Get-ChildItem -Path C:\ -Include interesting-file* -File -Recurse -ErrorAction SilentlyContinue

# Read file(s)
Get-ChildItem -Path C:\ -Include interesting-file* -File -Recurse -ErrorAction SilentlyContinue | Get-Content

# Count
(Get-Command | Where-Object -Property CommandType -Eq Cmdlet).count

# MD5, SHA1, SHA256, ...
Get-FileHash -Algorithm MD5 .\interesting-file.txt.txt

# pwd
Get-Location

# List cron
Get-ScheduledTask

# b64 decode
[Text.Encoding]::ASCII.GetString([Convert]::FromBase64String('azertyuiop'))

# User enumeration
Get-LocalUser

# Network info
Get-NetIPAddress

# Open ports (Listen, etc.)
Get-NetTCPConnection
```

# Verbs

## Common Verbs
-------------------------------------------------------------------------------------------------------------------------------------------------------
| Verb (alias)     | Action                                                                                                                           |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Add (a)          | Adds a resource to a container, or attaches an item to another item.                                                             |
| Clear (cl)       | Removes all the resources from a container but does not delete the container.                                                    |
| Close (cs)       | Changes the state of a resource to make it inaccessible, unavailable, or unusable.                                               |
| Copy (cp)        | Copies a resource to another name or to another container.                                                                       |
| Enter (et)       | Specifies an action that allows the user to move into a resource.                                                                |
| Exit (ex)        | Sets the current environment or context to the most recently used context.                                                       |
| Find (fd)        | Looks for an object in a container that is unknown, implied, optional, or specified.                                             |
| Format (f)       | Arranges objects in a specified form or layout.                                                                                  |
| Get (g)          | Specifies an action that retrieves a resource.                                                                                   |
| Hide (h)         | Makes a resource undetectable.                                                                                                   |
| Join (j)         | Combines resources into one resource.                                                                                            |
| Lock (lk)        | Secures a resource.                                                                                                              |
| Move (m)         | Moves a resource from one location to another.                                                                                   |
| New (n)          | Creates a resource. (The Set verb can also be used when creating a resource that includes data.)                                 |
| Open (op)        | Changes the state of a resource to make it accessible, available, or usable.                                                     |
| Optimize (om)    | Increases the effectiveness of a resource.                                                                                       |
| Pop (pop)        | Removes an item from the top of a stack.                                                                                         |
| Push (pu)        | Adds an item to the top of a stack.                                                                                              |
| Redo (re)        | Resets a resource to the state that was undone.                                                                                  |
| Remove (r)       | Deletes a resource from a container.                                                                                             |
| Rename (rn)      | Changes the name of a resource.                                                                                                  |
| Reset (rs)       | Sets a resource back to its original state.                                                                                      |
| Resize(rz)       | Changes the size of a resource.                                                                                                  |
| Search (sr)      | Creates a reference to a resource in a container.                                                                                |
| Select (sc)      | Locates a resource in a container. For example, the Select-String cmdlet finds text in strings and files.                        |
| Set (s)          | Replaces data on an existing resource or creates a resource that contains some data.                                             |
| Show (sh)        | Makes a resource visible to the user.                                                                                            |
| Skip (sk)        | Bypasses one or more resources or points in a sequence.                                                                          |
| Split (sl)       | Separates parts of a resource.                                                                                                   |
| Step (st)        | Moves to the next point or resource in a sequence.                                                                               |
| Switch (sw)      | Specifies an action that alternates between two resources, such as to change between two locations, responsibilities, or states. |
| Undo (un)        | Sets a resource to its previous state.                                                                                           |
| Unlock (uk)      | Releases a resource that was locked.                                                                                             |
| Watch (wc)       | Continually inspects or monitors a resource for changes.                                                                         |
-------------------------------------------------------------------------------------------------------------------------------------------------------

## Communications Verbs
-------------------------------------------------------------------------------------------------------------------------------------------------------
| Verb (alias)     | Action                                                                                                                           |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Connect (cc)     | Creates a link between a source and a destination.                                                                               |
| Disconnect (dc)  | Breaks the link between a source and a destination.                                                                              |
| Read (rd)        | Acquires information from a source.                                                                                              |
| Receive (rc)     | Accepts information sent from a source.                                                                                          |
| Send (sd)        | Delivers information to a destination.                                                                                           |
| Write (wr)       | Adds information to a target.                                                                                                    |
-------------------------------------------------------------------------------------------------------------------------------------------------------

## Data Verbs
-------------------------------------------------------------------------------------------------------------------------------------------------------
| Verb (alias)     | Action                                                                                                                           |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Backup (ba)      | Stores data by replicating it.                                                                                                   |
| Checkpoint (ch)  | Creates a snapshot of the current state of the data or of its configuration.                                                     |
| Compare (cr)     | Evaluates the data from one resource against the data from another resource.                                                     |
| Compress (cm)    | Compacts the data of a resource.                                                                                                 |
| Convert (cv)     | Changes the data from one representation to another. (Only for cmdlet supporting conversion.)                                    |
| ConvertFrom (cf) | Converts one primary type of input (the cmdlet noun indicates the input) to one or more supported output types.                  |
| ConvertTo (ct)   | Converts from one or more types of input to a primary output type. (The cmdlet noun indicates the output type.)                  |
| Dismount (dm)    | Detaches a named entity from a location.                                                                                         |
| Edit (ed)        | Modifies existing data by adding or removing content.                                                                            |
| Expand (en)      | Restores the data of a resource that has been compressed to its original state.                                                  |
| Export (ep)      | Encapsulates the primary input into a persistent data store, such as a file, or into an interchange format.                      |
| Group (gp)       | Arranges or associates one or more resources.                                                                                    |
| Import (ip)      | Creates a resource from data that is stored in a persistent data store (such as a file) or in an interchange format.             |
| Initialize (in)  | Prepares a resource for use, and sets it to a default state.                                                                     |
| Limit (l)        | Applies constraints to a resource.                                                                                               |
| Merge (mg)       | Creates a single resource from multiple resources.                                                                               |
| Mount (mt)       | Attaches a named entity to a location.                                                                                           |
| Out (o)          | Sends data out of the environment. For example, the Out-Printer cmdlet sends data to a printer.                                  |
| Publish (pb)     | Makes a resource available to others.                                                                                            |
| Restore (rr)     | Sets a resource to a predefined state, such as a state set by Checkpoint.                                                        |
| Save (sv)        | Preserves data to avoid loss.                                                                                                    |
| Sync (sy)        | Assures that two or more resources are in the same state.                                                                        |
| Unpublish (ub)   | Makes a resource unavailable to others.                                                                                          |
| Update (ud)      | Brings a resource up-to-date to maintain its state, accuracy, conformance, or compliance.                                        |
-------------------------------------------------------------------------------------------------------------------------------------------------------

## Diagnostic Verbs
-------------------------------------------------------------------------------------------------------------------------------------------------------
| Verb (alias)     | Action                                                                                                                           |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Debug (db)       | Examines a resource to diagnose operational problems.                                                                            |
| Measure (ms)     | Identifies resources that are consumed by a specified operation, or retrieves statistics about a resource.                       |
| Ping (pi)        | Deprecated - Use the Test verb instead.                                                                                          |
| Repair (rp)      | Restores a resource to a usable condition                                                                                        |
| Resolve (rv)     | Maps a shorthand representation of a resource to a more complete representation.                                                 |
| Test (t)         | Verifies the operation or consistency of a resource.                                                                             |
| Trace (tr)       | Tracks the activities of a resource.                                                                                             |
-------------------------------------------------------------------------------------------------------------------------------------------------------

## Lifecycle Verbs
-------------------------------------------------------------------------------------------------------------------------------------------------------
| Verb (alias)     | Action                                                                                                                           |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Approve (ap)     | Confirms or agrees to the status of a resource or process.                                                                       |
| Assert (as)      | Affirms the state of a resource.                                                                                                 |
| Build (bd)       | Creates an artifact (usually a binary or document) out of some set of input files. This verb was added in PowerShell 6.          |
| Complete (cp)    | Concludes an operation.                                                                                                          |
| Confirm (cn)     | Acknowledges, verifies, or validates the state of a resource or process.                                                         |
| Deny (dn)        | Refuses, objects, blocks, or opposes the state of a resource or process.                                                         |
| Deploy (dp)      | Sends an application, website, or solution to a remote target[s]. This verb was added in PowerShell 6.                           |
| Disable (d)      | Configures a resource to an unavailable or inactive state.                                                                       |
| Enable (e)       | Configures a resource to an available or active state.                                                                           |
| Install (is)     | Places a resource in a location, and optionally initializes it.                                                                  |
| Invoke (i)       | Performs an action, such as running a command or a method.                                                                       |
| Register (rg)    | Creates an entry for a resource in a repository such as a database.                                                              |
| Request (rq)     | Asks for a resource or asks for permissions.                                                                                     |
| Restart (rt)     | Stops an operation and then starts it again.                                                                                     |
| Resume (ru)      | Starts an operation that has been suspended.                                                                                     |
| Start (sa)       | Initiates an operation.                                                                                                          |
| Stop (sp)        | Discontinues an activity.                                                                                                        |
| Submit (sb)      | Presents a resource for approval.                                                                                                |
| Suspend (ss)     | Pauses an activity.                                                                                                              |
| Uninstall (us)   | Removes a resource from an indicated location.                                                                                   |
| Unregister (ur)  | Removes the entry for a resource from a repository.                                                                              |
| Wait (w)         | Pauses an operation until a specified event occurs.                                                                              |
-------------------------------------------------------------------------------------------------------------------------------------------------------

## Security Verbs
-------------------------------------------------------------------------------------------------------------------------------------------------------
| Verb (alias)     | Action                                                                                                                           |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Block (bl)       | Restricts access to a resource.                                                                                                  |
| Grant (gr)       | Allows access to a resource.                                                                                                     |
| Protect (pt)     | Safeguards a resource from attack or loss.                                                                                       |
| Revoke (rk)      | Specifies an action that does not allow access to a resource.                                                                    |
| Unblock (ul)     | Removes restrictions to a resource.                                                                                              |
| Unprotect (up)   | Removes safeguards from a resource that were added to prevent it from attack or loss.                                            |
-------------------------------------------------------------------------------------------------------------------------------------------------------

## Other Verbs
-------------------------------------------------------------------------------------------------------------------------------------------------------
| Verb (alias)     | Action                                                                                                                           |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Use (u)          | Uses or includes a resource to do something.                                                                                     |
-------------------------------------------------------------------------------------------------------------------------------------------------------
