# Music-streaming-System
Data Structures And Its Applications Assignment-1: Linear Data Structures

1. Song: Each song is identified by a unique non-negative integer identifier.
2. Playlist: A playlist is a collection of songs. We can add songs, delete songs and search for songs from it.
3. Play Queue: A song queue, which specifies the prioritised order in which the songs need to play next. If the queue is non-empty, the next song to be played is always from this queue and not from the playlist.
4. Shuffling: Shuffle the order of songs stored in the playlist. Shuffling is done by a combination of KSwap and reverse operations.
5. KSwap: Given an integer k, swap the node at position i with the node at position i+k up to the point where i+k is less than the size of the linked list i.e swap for the nodes that satisfy: 0 <= i+k < n where n is the length of the linked list, given 0 <= i < n and 0 <= k < n

Choice of data structures for implementing the problem at hand:
1) Playlist: The ideal data structure of choice for modelling a playlist would be a doubly linked list. This would come in handy as new songs can be added or the old ones can be removed from the playlist at any point in a doubly linked list. Also, it should support playing(querying) the previous song, next song and (current + i)’th song on the playlist.
2) Play Queue: A queue abstract data-type to follow FIFO. The choice of implementation of the ADT can be either a linked list or an array. For this assignment, we stick on to the linked list implementation of the queue as it gives us the flexibility of dynamically changing the size of the data structure.

1. dll.c:
a. Implementation file for all the basic doubly linked lists operations.
i. void insert_front(list_t* list, int data); // inserts data to the
beginning of the linked list
ii. void insert_back(list_t* list, int data); // inserts data to the end of
the linked list
iii. void insert_after(list_t* list, int data, int prev); // inserts data after
the node with data as “prev”
iv. void delete_front(list_t* list); // delete the start node from the linked
list.
v. void delete_back(list_t* list); // delete the end node from the linked
list.
vi. void delete_node(list_t* list, int data); // delete the first occurrence
of the node with data as “data” from the linked list.
vii. node_t* search(list_t* list, int data); // returns the pointer to the
node with data as “data” field

2. queue.c: // make use of the already implemented functions in dll.c
a. Implementation file for all the basic queue operations: (Students have the
liberty to either use array or linked list implementation of the queue abstract
data type)
i. void enqueue(queue_t* q, int data); // insert data to the queue
ii. int dequeue(queue_t* q); // return the data at the front of a queue
and also delete it. Return -1 if queue is empty
iii. int front(queue_t* q); // return the data at the front of a queue. Return
-1 if the queue is empty

3. music_player.c: // make use of the functions in dll.c and queue.c
a. Implementation file for all the music player platform operations:
i. void add_song(playlist_t* list, int song_id, int where); // add a
song to the playlist:
1. If where is -1, add the song to the start of the playlist
2. If where is -2, add the song to the end of the playlist
3. If where is non-negative, add the song after the song with
id = where in the playlist.

ii. void delete_song(playlist_t* playlist, int song_id); // remove the
song with given song id from the playlist
iii. song_t* search_song(playlist_t* playlist, int song_id); // return a
pointer to the node where the song_id is present in the playlist
iv. void play_next(playlist_t* playlist, music_queue_t* q); // play the
next song in the linked list with reference to the last played song or
play from the queue considering the following rules:
1. play the next song in the linked list if the queue is empty.
2. If the queue is not empty, play from the queue rather than the
next song in the list.
3. If there was no song that was played last, play the first song on
the list.
4. If there is no next song in the playlist, play the first song of the
playlist and follow the list order for further play_next calls.
5. If there are no songs yet in the playlist, return from the function
without doing anything.

v. void play_previous(playlist_t* playlist); // play the previous song in
the linked list with reference to the last played song.
1. If the previous song in the playlist is not present, play the last
song of the list and follow the reverse order of the list from the
last song for further play_previous calls.
2. No need to check for previously played songs from the
queue(would have been removed from the queue), i.e always
play the previous song from the playlist when this function is
called.
3. If there was no song that was played last, play the last song on
the list.
4. If there are no songs yet in the playlist, return from the function
without doing anything.

vi. void search_and_play(playlist_t* playlist, int song_id); // play the
song with the given song_id from the list(no need to bother about the
queue. Call to this function should always play the given song and
further calls to play_next and play_previous)
vii. void play_from_queue(playlist_t* q); // play a song from the queue
viii. void insert_to_queue(music_queue_t* q, int song_id); // insert a
song id to the queue
ix. void reverse(playlist_t* playlist); // reverse the order of the songs in
the given playlist. (Swap the nodes, not data)
x. void k_swap(playlist_t* playlist); // swap the node at position i with
the node at position i+k up to the point where i+k is less than the size
of the linked list
xi. void shuffle(playlist_t* playlist, int k); // perform k_swap and
reverse in the order k_swap first and reverse next.
xii. song_t* debug(playlist_t* playlist); // if the given linked list has a
cycle, return the start of the cycle, else return null. Check cycles only
in the forward direction i.e with the next pointer. No need to check for
cycles in the backward pointer.
