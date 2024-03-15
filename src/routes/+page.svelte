<script lang="ts">
    import { Button } from "$lib/components/ui/button";
    import { Input } from "$lib/components/ui/input";
    import * as Table from "$lib/components/ui/table";
    import { FontAwesomeIcon } from "@fortawesome/svelte-fontawesome";
    import { faTrash } from "@fortawesome/free-solid-svg-icons";
    
    let todo = '';
    let todos = [];

    function addTodo() {
        if (todo.trim() !== '') {
            todos = [...todos, todo];
            todo = '';
        }
    }

    function deleteTodo(index) {
        todos = todos.filter((_, i) => i !== index);
    }
</script>
<div class="flex items-center justify-center">
<h1>To Do or to Don't</h1>
</div>
<div class="flex items-center justify-center">
<Input bind:value={todo} placeholder="enter todo" class="max-w-xs" on:keydown={(e) => e.key === 'Enter' && addTodo()} />
</div>

<div class="w-3/4 mx-auto">
<Table.Root>
    {#if todos.length === 0}
  <Table.Caption>A list of your items.</Table.Caption>
    {/if}
    <Table.Header>
        <Table.Row>
            <Table.Head>List Items</Table.Head>
            <Table.Head>Action</Table.Head>
        </Table.Row>
    </Table.Header>
    <Table.Body>
        {#each todos as item, index (item)}
            <Table.Row>
                <Table.Cell class="font-medium">{item}</Table.Cell>
                <Table.Cell>
                    <button on:click={() => deleteTodo(index)}>
                        <FontAwesomeIcon icon={faTrash} />
                    </button>
                </Table.Cell>
            </Table.Row>
        {/each}
    </Table.Body>
</Table.Root>
</div>