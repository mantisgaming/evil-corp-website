<script>
    let mediaItemsList = $state([
        {
            title: "Invention Blueprint - Fragment #2",
            postedBy: "Employee #152",
            time: "2 hours ago",
            imageUrl: '/temp_bike_image.jpg',
            description: "The most recent blueprint piece found by faculty. Will be deleted soon, so make sure to download and preserve."
        }
    ]);

    function getCurrentDate() {
        const date = new Date();
        return date.toLocaleDateString('en-US', { 
            weekday: 'long', 
            year: 'numeric', 
            month: 'long', 
            day: 'numeric' 
        });
    }
</script>

<div class="media-library-container">
    <p class="current-date">{getCurrentDate()}</p>
    
    <div class="media-grid">
        {#each mediaItemsList as item}
            <div class="media-card">
                <div class="media-image-wrapper">
                    <img src={item.imageUrl} alt={item.title} />
                </div>
                <div class="media-info">
                    <h3>{item.title}</h3>
                    <p class="media-meta">Posted by <strong>{item.postedBy}</strong> • {item.time}</p>
                    <p class="media-description">{item.description}</p>
                </div>
            </div>
        {/each}
    </div>
</div>

<style lang="scss">
    .media-library-container {
        padding-top: 1rem;

        .current-date {
            font-size: 0.95rem;
            color: #7f8c8d;
            margin-bottom: 2rem;
        }

        .media-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
            gap: 2rem;
        }

        .media-card {
            background-color: white;
            border: 1px solid #bdc3c7;
            border-radius: 4px;
            overflow: hidden;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            transition: transform 0.2s ease;

            &:hover {
                transform: translateY(-4px);
            }

            .media-image-wrapper {
                width: 100%;
                height: 200px;
                background-color: #2c3e50; // Dark background if image fails to load
                display: flex;
                justify-content: center;
                align-items: center;

                img {
                    width: 100%;
                    height: 100%;
                    object-fit: cover; // Ensures the blueprint fills the box nicely
                }
            }

            .media-info {
                padding: 1.5rem;

                h3 {
                    margin: 0 0 0.5rem 0;
                    color: #2c3e50;
                    font-size: 1.1rem;
                    font-weight: bold;
                }

                .media-meta {
                    font-size: 0.85rem;
                    color: #95a5a6;
                    margin-bottom: 1rem;
                }

                .media-description {
                    font-size: 0.9rem;
                    color: #34495e;
                    line-height: 1.4;
                    margin: 0;
                }
            }
        }
    }
</style>