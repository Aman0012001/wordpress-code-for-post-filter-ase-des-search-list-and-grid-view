# wordpress-code-for-post-filter-ase-des-search-list-and-grid-view
custom code with pagination post fetch feachred image tittle and grid and list view catageries buttton  for home health care project

function custom_buttons_shortcode()
{
	ob_start(); ?>

	<?php
	// Assuming you have a function to fetch and display posts based on the view mode
	function displayPosts($viewMode)
	{
//code for pass variable 
		$search_query = query_posts('privatevar=myvalue') ?? '';

		// Example:
		$posts = get_posts(); // Replace this with your actual code to fetch pos
			}
	// Check if the view mode is set in the URL
	?>
	<div class="myflec">
<div class="mkctext">
<h3>
	Filter
	</h3>
		</div>
		<div class="container">
			<button class="listcatgbutton">
				Grid View
			</button>
			<div class="ebtn-group2">
				<button class="listbutton123">List view</button>
			</div>
		</div>

		<div class="container" meth>
		<button class="main-button" style="width:184px;background-color:#53D780;">Sort By</button>
			<div class="myfocus">
					<form method="post" action="?sort=asc">
			<button type="submit" class="button123">
				<span class="button12">Ascending Order</span>
			</button>
		</form>
		<button class="button123" action="?sort=des">
  			  <a href="?sort=desc" class="button12">Descending Order</a>
				</button>
		</div>
			</div>
		<div class="container">
			<button class="catgbutton" >
				catagory
			</button>
			<div class="btn-group2">		
		<?php
				// Your PHP code to fetch and display post categories goes here
				$categories = get_categories();
				foreach ($categories as $category) {
				echo '<button class="button12" style="margin-top:4px;"><a href="?category=' . htmlspecialchars($category->slug)   . '">' . htmlspecialchars($category->name) . '</a></button>';} 
				?>
</div>
</div>
<!-- search field -->
<div class="container">
  <div class="container1">
    <form role="search"  id="searchform" class="searchform" action="<?php echo home_url( '/' ); ?>">
      <input type="text" value="" name="s" class="myblog-search">
      <input type="submit" class="my-blog-search" value="<?php the_search_query();?>">
    </form>
  </div>
</div>
		</div>
<!-- 	</div> -->
	<div class="my-containeqqr">
		        <?php
     $paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
	$sortOrder = isset($_GET['sort']) ? strtolower($_GET['sort']) : 'asc';
// 	in code add a posts 
	$category_filter = isset($_GET['category']) ? sanitize_text_field($_GET['category']) : '';
	$args = array(
    'orderby'        => 'title',
    'order'          => $sortOrder,
    'paged'          => $paged,
    'posts_per_page' => 8,
    's'              => $_POST['search'], // Include this line to search for a specific term
    'category_name'   => $category_filter, // Add this line to include the category filter
	);
	$posts = get_posts($args);
	foreach ($posts as $post) {
    $counter++;
			// Display your post content here
			echo'<div class="myliccst">';
			echo '<div class="myblog-postcon">';
			echo get_the_post_thumbnail($post->ID, 'thumbnail', array('class' => 'blog-post-img'));
			echo '<div class="mainblogcont">';
			$post_date = get_the_date('l F j | Y', $post->ID);
			echo '<div class="asdate">' . $post_date . '</div>';
			echo '<div class="blog-title1">' . $post->post_title . '</div>';
			$trimmed_content = wp_trim_words($post->post_content, 15, '...');
			echo '<div class="post-content1234">' . $trimmed_content . ' <a href="' . get_permalink($post->ID) . '" class="redmoret">Read More</a></div>';
			echo "</div>";
			echo "</div>";
			echo "</div>";
			$counter++; // Increment the counter after each post
		}
		?>
	</div>
	</div>
	<div class="my-containeqqrss">

		<?php
		// Your PHP code to fetch and display posts goes here
		// Pagination
		$total_pages = ceil(wp_count_posts()->publish / 8); // Assuming 8 posts per page
		$big = 999999999; // need an unlikely integer

		echo '<div class="pagination">';
		echo paginate_links(array(
			'base'      => str_replace($big, '%#%', esc_url(get_pagenum_link($big))),
			'format'    => '?paged=%#%',
			'current'   => max(1, $paged),
			'total'     => $total_pages,
			'prev_text' => '&laquo Previous	',
			'next_text' => 'Next &raquo;',
			'prev_next' => true, // Disable the default previous and next links
			'class'     => 'pagination-links',

		));
		echo '</div>';
		?>
	</div>
<?php
	return ob_get_clean();
}
// code for list post design 
add_shortcode('custom_buttons', 'custom_buttons_shortcode');
