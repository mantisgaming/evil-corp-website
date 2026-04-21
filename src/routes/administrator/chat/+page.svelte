<script lang="ts">
    import { onMount } from 'svelte';

    const userGroups = [
        { role: "Administrator", color: "#e74c3c", members: ["Archibald Geyser"] },
        { role: "Moderators", color: "#f1c40f", members: ["Employee #005", "Employee #047"] },
        { role: "Users", color: "#95a5a6", members: ["Employee #025", "Employee #088", "Employee #093", "Employee #127", "Employee #152", "Employee #171", "Employee #202", "Employee #213", "Employee #218", "{Unknown User}"] }
    ];

    const defaultMessages = [
        {
            name: "Employee #047",
            profile: "👤",
            message: "Keep any conversations like this verbel, and make sure the blueprint is deleted after being up for 24 hours. The less of a trace we leave, the better.",
            time: "2 hours ago"
        },
        {
            name: "Employee #093",
            profile: "👤",
            message: "Upload them to the Media Library tab. Don't worry, the public won't be able to see them, only us.",
            time: "3 hours ago"
        },
        {
            name: "Employee #152",
            profile: "👤",
            message: "Where are we storing pieces of blueprints we've found? I was told to put them here in the backend somewhere.",
            time: "3 hours ago"
        }
    ];

    let chatMessages = $state([...defaultMessages]);

    onMount(() => {

        const savedChat = window.localStorage.getItem('solcorp_chat_history');
        if (savedChat) {
            chatMessages = JSON.parse(savedChat);
        }

        const addMessageAndSave = (msg: any) => {

            if (!chatMessages.find(m => m.message === msg.message)) {
                chatMessages = [msg, ...chatMessages];
                window.localStorage.setItem('solcorp_chat_history', JSON.stringify(chatMessages));
            }
        };

        const timer1 = setTimeout(() => {
            addMessageAndSave({ 
                name: "Employee #218", 
                profile: "👤", 
                message: "Who is {Unknown User}? I didn't know we could have invalid names like that.", 
                time: "just now" 
            });
        }, 15000);

        const timer2 = setTimeout(() => {
            addMessageAndSave({ 
                name: "Employee #005", 
                profile: "👤", 
                message: "We shouldn't be able to. Someone notify Archibald about this immediately.", 
                time: "just now" 
            });
        }, 20000);

        return () => {
            clearTimeout(timer1);
            clearTimeout(timer2);
        };
    });

    function getCurrentDate() {
        const date = new Date();
        return date.toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
    }
</script>

<div class="chat-logs-container">
    <h2 class="current-date">{getCurrentDate()}</h2>
    
    <div class="chat-layout-wrapper">
        <div class="chat-boxes">
            {#each chatMessages as chat}
                <div class="chat-box">
                    <div class="profile-header">
                        <div class="profile-info">
                            <span class="profile-icon">{chat.profile}</span>
                            <span class="profile-name">{chat.name}</span>
                        </div>
                        <span class="chat-time">{chat.time}</span>
                    </div>
                    <p class="chat-message">{chat.message}</p>
                </div>
            {/each}
        </div>

        <aside class="user-list-sidebar">
            {#each userGroups as group}
                <div class="user-group">
                    <h3 style="color: {group.color}">{group.role} — {group.members.length}</h3>
                    {#each group.members as member}
                        <div class="user-item">
                            <span class="user-status-icon">👤</span>
                            <span class="user-name">{member}</span>
                        </div>
                    {/each}
                </div>
            {/each}
        </aside>
    </div>
</div>

<style lang="scss">

    .chat-logs-container {
        padding-top: 1rem;

        h2.current-date {
			color: #2c3e50;
			margin-top: 0;
			font-size: 1.5rem;
		}

		p {
			color: #7f8c8d;
			margin-bottom: 0;
		}

        .current-date {
            font-size: 0.95rem;
            color: #7f8c8d;
            margin-bottom: 2rem;
        }

        .chat-layout-wrapper {
            display: flex; 
            flex-direction: row;
            align-items: flex-start;
            gap: 2rem;
            width: 100%;
        }

        .chat-boxes {
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
            flex: 1;

            .chat-box {
                background-color: white;
                border: 1px solid #bdc3c7;
                border-radius: 4px;
                padding: 1.5rem;
                box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);

                .profile-header {
                    display: flex;
                    align-items: center;
                    justify-content: space-between;
                    margin-bottom: 0.5rem;

                    .profile-info {
                        display: flex;
                        align-items: center;
                        gap: 0.75rem;

                        .profile-icon {
                            font-size: 1.5rem;
                        }

                        .profile-name {
                            font-weight: bold;
                            color: #2c3e50;
                            font-size: 1rem;
                        }
                    }

                    .chat-time {
                        font-size: 0.85rem;
                        color: #95a5a6;
                    }
                }

                .chat-message {
                    color: #34495e;
                    margin: 0;
                    font-size: 0.95rem;
                    line-height: 1.5;
                }
            }
        }

        .user-list-sidebar {
            width: 400px;
            background-color: #f8f9fa;
            border-radius: 4px;
            padding: 1rem;
            border: 1px solid #bdc3c7;
            position: sticky;
            top: 0;
            flex-shrink: 0;

            .user-group {
                margin-bottom: 1.5rem;

                h3 {
                    font-size: 1.2rem;
                    text-transform: uppercase;
                    letter-spacing: 1px;
                    margin-bottom: 0.5rem;
                    border-bottom: 1px solid #eee;
                    padding-bottom: 0.25rem;
                }
            }

            .user-item {
                display: flex;
                align-items: center;
                gap: 0.5rem;
                padding: 0.25rem 0;
                
                .user-status-icon {
                    font-size: 0.9rem;
                    opacity: 0.7;
                }

                .user-name {
                    font-size: 1.2rem;
                    color: #2c3e50;
                }
            }
        }
    }
</style>